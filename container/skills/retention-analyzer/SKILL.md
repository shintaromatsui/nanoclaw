---
name: retention-analyzer
description: Customer retention and churn analysis with cohort tables, churn calculations, and intervention recommendations. Use when someone says "retention analysis", "churn analysis", "cohort analysis", "why are we losing customers", "customer retention", "churn rate", "retention curve", "logo churn", "revenue churn", or needs to understand retention patterns.
---

# Retention & Churn Analyzer

Diagnose retention patterns with cohort analysis, churn decomposition, and intervention recommendations.

## Input

Parse the message to extract:
- **Data** (required): Customer/revenue data by cohort or period, or a situation description
- **Analysis type** (optional): cohort, churn-rate, drivers, benchmarks, full (default: full)
- **Segment** (optional): Break down by segment (enterprise, SMB, etc.)

Examples:
- "we started with 500 customers, added 200, lost 80. ARR went from $5M to $6.5M"
- "cohort analysis for Q1-Q4 signups"
- "why are enterprise customers churning at 15%"
- "churn benchmarks for B2B SaaS at $50K ACV"

## Process

### Step 1: Calculate Core Metrics

```
*Churn Metrics*

• Gross logo churn (annual): XX% [benchmark: 5-7%] [status]
• Net revenue churn (MRR): XX% [benchmark: <1% monthly] [status]
• Net Revenue Retention: XXX% [>110% good, >120% great] [status]
• Expansion rate: XX%
• Avg customer lifetime: XX months
```

### Step 2: Cohort Retention Table

```
*Cohort Retention* (% retained)

Jan: 100% → 85% → 78% → 72% → 68% → 62%
Feb: 100% → 82% → 74% → 69% → 65% → 58%
Mar: 100% → 88% → 81% → 76% → 72% → 66%
Apr: 100% → 90% → 84% → 79% → 75%

*Observations:*
• Biggest drop: M0→M1 (avg -15%) — activation problem
• Stabilizes around M4-M5
• Mar-Apr cohorts retaining better — investigate what changed
```

### Step 3: Identify Patterns

*When customers leave:*
- XX% in months 1-3 (activation failure)
- XX% at contract renewal (value gap)
- XX% steady-state (competitive/need change)

*Who leaves most:*
- Segment comparison
- ACV correlation
- Acquisition channel quality

### Step 4: Root Cause Hypotheses

For each primary churn driver:

```
*Churn Driver 1: [e.g., Early activation failure]*
Evidence: XX% of churn in M1-M3
Likely cause: [hypothesis]
Intervention: [specific recommendation]
Expected impact: Reduce M1-M3 churn by XX%

*Churn Driver 2: [e.g., Renewal gap]*
[same format]
```

### Step 5: Benchmark Comparison

Use web research if needed to pull relevant benchmarks:

```
*Benchmarks*

• NRR: Yours XXX% vs benchmark >120% — [gap]
• Gross churn: Yours XX% vs benchmark 5-7% — [gap]
• Expansion: Yours XX% vs benchmark >30% — [gap]

Position: [Above/At/Below] peer benchmarks
```

### Step 6: Interventions

```
*Recommended Interventions*

1. [e.g., Redesign onboarding to drive key action in 48 hours]
   Target: M1 retention | Expected: +5-8% | Effort: Medium

2. [e.g., Proactive outreach 60 days before renewal]
   Target: Renewal churn | Expected: -3% | Effort: Low

3. [e.g., Launch expansion playbook for enterprise]
   Target: NRR | Expected: +10% | Effort: High

*Quick wins (this week):*
• [Action]
• [Action]

*Metrics to track:*
• [Leading indicator] — check [frequency]
```

## Design Principles

- **Revenue churn > logo churn.** Losing 10 $1K customers differs from losing 1 $100K customer. Show both.
- **Cohort analysis is non-negotiable.** Blended rates hide everything.
- **Benchmarks without context are useless.** Same ACV range, same market, same stage.
- **Interventions must be specific.** "Improve onboarding" is not an intervention. "Drive [key action] within 48 hours" is.
- **Leading indicators > lagging.** By the time someone churns, it's too late. Find upstream signals.
