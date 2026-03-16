---
name: variance-analysis
description: Compare actuals against budget, forecast, or prior period with root cause hypotheses. Use when someone says "variance analysis", "actual vs budget", "what went off plan", "compare actuals to forecast", "budget variance", "why did we miss", "over budget", "under budget", "plan vs actual", or needs to understand deviations from expected performance.
---

# Variance Analysis

Compare actual results against budget/forecast/prior period. Identify what deviated, by how much, why, and what to do about it.

## Input

Parse the message to extract:
- **Data** (required): Actuals and the comparison baseline (budget, forecast, or prior period)
- **Period** (optional): Time period being analyzed (default: most recent)
- **Materiality threshold** (optional): % variance that warrants investigation (default: 10%)

The user can provide data by:
1. Typing/pasting numbers directly
2. Referencing a file path in `/workspace/group/`
3. Referencing KPI tracker data: "compare actuals from KPI tracker to Q1 budget"

Examples:
- "variance analysis: Revenue actual $2.1M vs budget $2.5M, COGS actual $800K vs budget $700K"
- "Q1 actuals vs plan — use KPI data"
- "last month vs same month last year"

## Process

### Step 1: Structure the Data

For each line item, calculate:
- Actual, Budget/Forecast/Prior, Variance ($), Variance (%), F/U status
- Revenue/income: Actual > Budget = Favorable
- Cost/expense: Actual < Budget = Favorable

### Step 2: Classify Variances

- *Material:* Variance % exceeds threshold → investigate
- *Immaterial:* Below threshold → note only
- Sort by absolute $ impact (largest first)

### Step 3: Hypothesize Root Causes

For each material variance, generate 2-3 plausible hypotheses:

Revenue drivers: Volume, Price, Timing, New/lost customers
Cost drivers: Volume-driven, Rate-driven, Timing, One-time items, Scope changes

Label each: Likely / Possible / Speculative

### Step 4: Build Output

```
*Variance Analysis: [Period]*
Actual vs [Budget/Forecast/Prior]
Threshold: [X]%

*Summary*
Total revenue: [actual] vs [budget] — [variance %] [F/U]
Total costs: [actual] vs [budget] — [variance %] [F/U]
Net: [actual] vs [budget] — [variance %] [F/U]

*Material Variances*

🔴 *Product A Revenue:* -$300K (-20.0%) UNFAVORABLE
Most likely: [hypothesis]
Action: [recommendation]

🔴 *Hosting Costs:* -$50K (-20.0%) UNFAVORABLE
Most likely: [hypothesis]
Action: [recommendation]

🟢 *Product B Revenue:* +$100K (+12.5%) FAVORABLE
Driver: [explanation]

*Top 3 Unfavorable*
1. [Item] — -[amount] — [explanation]
2. [Item] — -[amount] — [explanation]
3. [Item] — -[amount] — [explanation]

*Top 3 Favorable*
1. [Item] — +[amount] — [explanation]
2. [Item] — +[amount] — [explanation]
3. [Item] — +[amount] — [explanation]

*Corrective Actions*
1. [Action] — Owner: [TBD] — Due: [date]
2. [Action] — Owner: [TBD] — Due: [date]

*Forecast Implications*
[How these variances change the full-year outlook]
```

### Step 5: Persist

Store budget data in `/workspace/group/ops/budgets/[period].json` for trend-over-trend analysis. Link to KPI tracker data if available.

## Chaining

- For material unfavorable variances, suggest root-cause analysis
- For forward projections, suggest scenario modeling
- For audience-specific packaging, suggest stakeholder-report

## Design Principles

- **Favorable/Unfavorable, not positive/negative.** Revenue up = favorable. Costs up = unfavorable.
- **Materiality focuses attention.** Don't waste time on 2% variances when there's a 20% miss.
- **Hypotheses, not conclusions.** Label confidence levels.
- **Actions are mandatory.** Every material unfavorable variance needs a corrective action.
- **Forecast implications are the real output.** Past variance matters because it changes future expectations.
