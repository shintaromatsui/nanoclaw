---
name: cost-analyzer
description: Financial decision support — CBA, ROI, NPV, payback period, build-vs-buy, IRR. Use when someone says "cost-benefit analysis", "ROI on", "is this worth it", "build vs buy", "payback period", "NPV", "financial impact", "should we invest in", "TCO", or needs to evaluate the financial merits of a decision.
---

# Cost & Financial Analyzer

Structured financial decision support. Answer "is this worth it?" with numbers, not vibes.

## Input

Parse the message to extract:
- **Decision or investment** (required): What's being evaluated
- **Analysis type** (optional): CBA, ROI, build-vs-buy, TCO (default: infer)
- **Data** (optional): Known costs, revenues, timelines, assumptions
- **Time horizon** (optional): How far out to project (default: 3 years)
- **Discount rate** (optional): For NPV (default: 10%)

Examples:
- "ROI on hiring 2 more SDRs"
- "build vs buy for auth system"
- "is it worth switching from Salesforce to HubSpot"
- "CBA for opening a London office"

## Process

### Step 1: Frame the Decision

- *Option A:* The proposed investment/change
- *Option B:* Status quo or alternative
- *Decision criteria:* What makes this "worth it"?

### Step 2: Gather Costs

*One-time:* Implementation, training, migration, opportunity cost
*Recurring:* Licenses, headcount (1.3-1.5x base for fully loaded), maintenance
*Hidden:* Integration effort, productivity dip during transition, vendor lock-in

Label each: Known / Estimated / Assumed

### Step 3: Quantify Benefits

*Direct revenue:* New revenue, retained revenue, accelerated revenue
*Cost savings:* Headcount avoided, tool consolidation, process efficiency
*Strategic:* List but don't fabricate dollar values (competitive positioning, morale, optionality)

### Step 4: Build the Model

```
*Financial Analysis: [Decision]*
Time horizon: [X] years | Discount rate: [X]%

*Costs*
One-time: $XX (implementation, training, migration)
Year 1: $XX | Year 2: $XX | Year 3: $XX
Total 3-year cost: $XX

*Benefits*
Year 1: $XX | Year 2: $XX | Year 3: $XX
Total 3-year benefit: $XX

*Key Metrics*
• ROI: XX%
• NPV: $XX
• Payback period: XX months
• IRR: XX%

*Cumulative cash flow:*
Month 0: ($XX)
Month 6: ($XX)
Month 12: ($XX) ← breakeven ~month XX
Month 24: $XX
Month 36: $XX
```

### Step 5: Sensitivity Analysis

Test 2-3 most uncertain variables:

```
*Sensitivity*

If [variable] changes:
• Pessimistic: ROI = XX%, Payback = XX months
• Base case: ROI = XX%, Payback = XX months
• Optimistic: ROI = XX%, Payback = XX months

*Breakeven:* Investment works as long as [variable] stays above [threshold]
*Model breaks if:* [condition]
```

### Step 6: Build vs Buy (if applicable)

Side-by-side comparison: upfront cost, annual cost, 3-year TCO, time to value, customization, maintenance, switching cost, risk.

### Step 7: Recommendation

```
*Recommendation:* [Proceed / Do not proceed / Proceed with conditions]
*Confidence:* [High / Medium / Low]

*Why:* [2-3 sentences]

*Key assumptions that must hold:*
1. [Assumption] — if wrong, impact is [X]
2. [Assumption] — if wrong, impact is [X]

*Next steps:*
1. [Action] — Owner: [TBD] — By: [date]
2. [Action] — Owner: [TBD] — By: [date]
```

## Design Principles

- **Conservative estimates.** Understate benefits, overstate costs. If it still works, it's good.
- **Show the breakeven.** "What has to be true for this to be worth it" is the most useful output.
- **Hidden costs are real costs.** Migration, training, productivity dip, opportunity cost.
- **Qualitative matters but doesn't get fake numbers.** Don't assign $500K to "improved morale."
- **Sensitivity over precision.** A range is more honest than a point estimate.
