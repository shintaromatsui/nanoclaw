---
name: kpi-tracker
description: Track KPIs with targets, record actuals, compute trends, flag breaches. Use when someone says "track KPIs", "update metrics", "dashboard", "how are we tracking", "metric status", "log metric", "KPI dashboard", "are we on track", or needs persistent metric tracking with traffic-light status.
---

# KPI Tracker

Define KPIs with targets, record actuals over time, compute trends (WoW/MoM/QoQ), flag threshold breaches. Persistent — stores data as JSON.

## Input

Parse the message to extract the **action** and **parameters**:

**Actions:**
- **define** `[metric_name] target=[value] yellow=[threshold] red=[threshold] unit=[unit] frequency=[daily/weekly/monthly]`
- **log** `[metric_name]=[value]` or `[metric_name]=[value] date=[YYYY-MM-DD]`
- **dashboard** — Show all KPIs with traffic-light status
- **trend** `[metric_name]` — Show period-over-period trends
- **status** — Quick summary of RED/YELLOW metrics only

Examples:
- "define KPI MRR target=500000 yellow=450000 red=400000 unit=$ frequency=monthly"
- "log MRR=485000"
- "KPI dashboard"
- "how are we tracking on MRR"
- "any metrics off track?"

If the user just says "dashboard" or "how are we tracking" without specifics, show the current dashboard. If no KPIs are defined yet, walk them through defining their first set.

## Data Storage

Store all data in `/workspace/group/ops/metrics/`:

**`/workspace/group/ops/metrics/definitions.json`** — KPI definitions:
```json
{
  "metrics": {
    "MRR": {
      "name": "Monthly Recurring Revenue",
      "target": 500000,
      "yellow_threshold": 450000,
      "red_threshold": 400000,
      "unit": "$",
      "frequency": "monthly",
      "direction": "higher_is_better",
      "created": "2026-03-14"
    }
  }
}
```

**`/workspace/group/ops/metrics/actuals.json`** — Time-series data points:
```json
{
  "MRR": [
    {"date": "2026-01-01", "value": 420000},
    {"date": "2026-02-01", "value": 455000},
    {"date": "2026-03-01", "value": 485000}
  ]
}
```

On first use, create the directory and initialize both files if they don't exist.

## Process

### Action: define

1. Parse metric name, target, thresholds, unit, frequency
2. Infer `direction` — default `higher_is_better` unless metric name suggests otherwise (churn, cost, bug count = `lower_is_better`)
3. Read existing definitions.json (or initialize)
4. Add/update the metric definition
5. Write back
6. Confirm with the defined parameters

### Action: log

1. Parse metric name(s) and value(s). Support multiple: `MRR=485000 NPS=42 Churn=3.2%`
2. Default date to today if not specified
3. Read actuals.json, append data point(s), sort by date
4. Write back
5. For each logged metric, show current status vs target with traffic light

### Action: dashboard

1. Read both definitions.json and actuals.json
2. For each defined metric, compute:
   - Latest value (most recent data point)
   - Status: GREEN / YELLOW / RED based on thresholds
   - vs Target: absolute and percentage variance
   - Trend: % change from prior period
   - Run rate: projected value at current trajectory

Format for Telegram:

```
*KPI DASHBOARD* — [date]

*MRR* $485K | Target $500K | -3.0%
🟡 YELLOW | +6.6% MoM

*NPS* 42 | Target 50 | -16.0%
🔴 RED | -2.3% MoM

*Churn* 3.2% | Target <5% | OK
🟢 GREEN | +0.1% MoM

*ALERTS:*
🔴 NPS (42 vs 50) — declining 3 consecutive periods
🟡 MRR ($485K vs $500K) — on track to hit target by Apr
```

### Action: trend

1. Pull all data points for the specified metric
2. Compute period-over-period % change, 3-period moving average, run rate
3. Show trend table and projection

### Action: status

1. Filter to only RED and YELLOW metrics
2. Sort by severity (RED first), then by largest variance
3. If all GREEN: "All KPIs on track. No alerts."

## Chaining

- When a metric hits RED, suggest running root-cause analysis
- For financial metrics, suggest unit-economics analysis
- Suggest exporting to Google Sheet if the user wants to share

## Design Principles

- **Persistence is the point.** Always read/write the JSON files.
- **Traffic lights are instant clarity.** GREEN/YELLOW/RED parseable in 2 seconds.
- **Trends matter more than snapshots.** Always show direction.
- **Alert on what needs attention.** Don't bury problems in green.
- **Make logging frictionless.** "log MRR=485000" should be all you need.
