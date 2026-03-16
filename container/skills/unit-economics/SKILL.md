---
name: unit-economics
description: Analyze unit economics with CAC, LTV, payback, margins, and sensitivity tables. Use when someone says "unit economics", "does the math work", "CAC LTV", "payback period", "margin analysis", "business model analysis", "economics of", "is this business profitable", "revenue model", or needs to evaluate whether a business model or growth strategy is financially sound.
---

# Unit Economics Analysis

Break down a business to its fundamental economic unit. Does the math work? Where does it break?

## Input

Parse the message to extract:
- **Company or business model** (required): What to analyze
- **Data** (optional): Any known metrics (ARR, customers, pricing, churn, etc.)
- **Question** (optional): Specific angle — "can they sustain this growth?", "does freemium work here?", "is enterprise viable?"

Examples:
- "unit economics on Vanta at $300M ARR"
- "does the math work for a SaaS compliance business with freemium"
- "analyze our enterprise motion — is it working"
- "unit economics for a food delivery marketplace"

## Process

### Step 1: Gather Available Data

Check for existing research:
- `/workspace/extra/job-search/company-research/` for company-specific data
- Public sources: pricing pages, analyst reports, press releases

Use the research skill for:
- Pricing pages (critical for revenue per customer estimates)
- Analyst reports mentioning metrics
- Competitor benchmarks

**Label known vs. estimated data clearly. Never present estimates as facts.**

### Step 2: Define the Unit

What is the "unit" in this business?
- **SaaS:** One customer (or one seat, one contract)
- **Marketplace:** One transaction (or one active seller/buyer pair)
- **Consumer:** One user (or one paying subscriber)
- **Services:** One engagement

### Step 3: Build the Economic Model

**Revenue Side:**
- **ACV:** Average revenue per customer per year
- **ARPU:** Average revenue per user
- **Expansion revenue:** Net Revenue Retention
- **Gross margin:** Revenue minus direct costs

**Cost Side:**
- **CAC:** Total S&M spend ÷ new customers acquired
- **COGS:** Direct costs per customer (hosting, support, onboarding)
- **Servicing cost:** Ongoing cost to retain/support one customer per year

**Retention:**
- **Gross churn:** % of customers lost per year
- **Net revenue retention (NRR):** Revenue from existing cohort YoY (>100% = expansion)
- **Logo retention:** % of customers retained

**Derived Metrics:**
- **LTV:** (ACV × Gross Margin) ÷ Churn Rate
- **LTV:CAC Ratio:** LTV ÷ CAC (target: >3x for SaaS)
- **CAC Payback:** CAC ÷ (ACV × Gross Margin ÷ 12) months
- **Rule of 40:** Revenue growth % + profit margin % (target: >40%)
- **Burn Multiple:** Net burn ÷ Net new ARR (target: <2x)
- **Magic Number:** Net new ARR ÷ Prior quarter S&M spend (target: >0.75)

### Step 4: Build the Output Table

```
## Unit Economics: [Company/Model]

### Revenue Model
| Metric | Value | Source |
|--------|-------|--------|
| ARR | $X | [known/estimated] |
| Customers | X | [known/estimated] |
| ACV | $X | ARR ÷ Customers |
| NRR | X% | [known/estimated] |
| Gross Margin | X% | [known/estimated] |

### Acquisition
| Metric | Value | Source |
|--------|-------|--------|
| CAC (blended) | $X | [known/estimated] |
| CAC Payback | X months | Calculated |
| LTV | $X | Calculated |
| LTV:CAC | X:1 | Calculated |

### Efficiency
| Metric | Value | Benchmark | Verdict |
|--------|-------|-----------|---------|
| Rule of 40 | X | >40 | [good/watch/concern] |
| Burn Multiple | X | <2x | [good/watch/concern] |
| Magic Number | X | >0.75 | [good/watch/concern] |

### Verdict: [Healthy / Scaling / Strained / Broken]
```

### Step 5: Sensitivity Analysis

Build a sensitivity table on the 2 most impactful variables:

```
LTV:CAC Ratio at Different Churn / ACV Levels

              | ACV $20K | ACV $40K | ACV $60K |
| Churn 5%    |   X:1    |   X:1    |   X:1    |
| Churn 10%   |   X:1    |   X:1    |   X:1    |
| Churn 15%   |   X:1    |   X:1    |   X:1    |
| Churn 20%   |   X:1    |   X:1    |   X:1    |
```

Highlight where the model breaks (LTV:CAC < 1x) and where it's excellent (>5x).

### Step 6: Analysis & Implications

Answer:
- **Does the math work?** Is this a viable business at current scale?
- **Where does it break?** What variable, if it moves 20%, kills the model?
- **What drives improvement?** Top 2-3 levers to improve unit economics
- **How does it compare?** Benchmark against best-in-class in the category
- **Scaling dynamics:** Do unit economics improve or degrade at scale?

### Benchmarks Reference

**Best-in-class SaaS:**
- LTV:CAC > 5x, CAC Payback < 12 months, NRR > 120%, Gross Margin > 80%, Rule of 40 > 60, Burn Multiple < 1x

**Median SaaS:**
- LTV:CAC ~ 3x, CAC Payback ~ 18 months, NRR ~ 110%, Gross Margin ~ 70-75%, Rule of 40 ~ 30-40, Burn Multiple ~ 2-3x

## Output Format

```
# Unit Economics: [Company/Model]

**Bottom line:** [1 sentence — does the math work?]

## The Unit
[What the economic unit is and how the business makes money. 2-3 sentences.]

## Model
[Tables from Step 4]

## Sensitivity
[Table from Step 5]

## Analysis
[What works, what breaks, what to improve]

## Key Assumptions
[Bullet list with confidence levels — always label known vs. estimated]
```

## Design Principles

- **Label known vs. estimated.** Never present guesses as facts.
- **Sensitivity > point estimates.** A range of outcomes is more useful than a single number.
- **Benchmarks give meaning.** "LTV:CAC of 4x vs. 3x median" is useful. "4x" alone is not.
- **Find the breakpoint.** The most useful output is "this model breaks if churn exceeds X%."
- **Simple model > complex model.** A 5-variable model you understand beats a 20-variable one you don't.
