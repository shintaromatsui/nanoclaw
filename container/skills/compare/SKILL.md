---
name: compare
description: Comparative analysis of 2-5 entities across weighted dimensions. Use when someone says "compare X vs Y", "which is better", "help me choose between", "side by side", "how do these stack up", "evaluate options", "rank these", or needs structured comparison of companies, roles, products, or strategies.
---

# Comparative Analysis

Build a rigorous, weighted comparison of multiple options to drive a decision.

## Input

Parse the message to extract:
- **Entities** (required): 2-5 things to compare (companies, roles, products, strategies)
- **Context** (optional): What the decision is for, constraints, priorities
- **Dimensions** (optional): Specific criteria — if not provided, auto-generate based on entity type

Examples:
- "compare Vanta vs Amplitude vs Cribl as next role"
- "compare these three offer packages" (then paste details)
- "compare React vs Svelte for our frontend"

## Process

### Step 1: Frame the Decision

Clearly state:
- **Decision:** What is being decided (1 sentence)
- **Decision-maker:** What Shintaro optimizes for (career capital, comp, learning, impact)
- **Constraints:** Non-negotiable requirements that eliminate options immediately

Check for existing research in `/workspace/extra/job-search/company-research/` before researching from scratch.

### Step 2: Define Dimensions & Weights

Create 5-8 evaluation dimensions. Auto-generate based on entity type if not specified:

**For companies/roles:**
- Comp (total package, equity upside, cash)
- Growth trajectory (revenue, market, team scaling)
- Role scope & impact (what you'd own, altitude, visibility)
- Learning & career capital (new skills, network, brand)
- Culture & leadership (CEO, team, values fit)
- Risk profile (funding, market, execution)
- Personal fit (location, lifestyle, energy)

**For products/tools:**
- Core capability (does it do the job?)
- Ease of adoption (learning curve, migration cost)
- Scalability (grows with needs)
- Ecosystem & integrations
- Cost (TCO over relevant timeframe)
- Future trajectory (roadmap, momentum)

**For strategies/approaches:**
- Expected impact (upside magnitude)
- Probability of success
- Time to results
- Resource requirements
- Reversibility (cost of being wrong)

Assign weights (must sum to 100%). Explain why things are weighted as they are.

### Step 3: Score Each Entity

For each entity × dimension:
1. Score 1-10 with a brief rationale (1-2 sentences)
2. Flag any scores where confidence is low

### Step 4: Build the Scorecard

```
## Scorecard

                    | Entity A | Entity B | Entity C |
| Dimension 1 (W%)  |  8 — why |  6 — why |  7 — why |
| Dimension 2 (W%)  |  7 — why |  9 — why |  5 — why |
| WEIGHTED TOTAL     |  7.4     |  7.1     |  6.2     |
```

### Step 5: Analysis

Synthesize beyond the scores:
- **Recommendation:** Clear winner with 1-sentence rationale
- **Key tradeoff:** The biggest thing you're giving up by choosing the winner
- **Upset scenario:** What would need to be true for #2 to win instead
- **Decision quality check:** What information would most change the ranking?

### Step 6: Sensitivity Check

- Which dimensions, if re-weighted, would flip the ranking?
- Are scores clustered (close call) or separated (clear winner)?
- Flag if the result is fragile (depends on 1-2 assumptions)

## Output Format

```
# [Entity A] vs [Entity B] vs [Entity C]

**Decision:** [What's being decided]
**Bottom line:** [Winner] wins on [X], but [Runner-up] is stronger on [Y]. Choose [Winner] if [condition]; choose [Runner-up] if [condition].

## Scorecard
[Table]

## Key Tradeoffs
- Choosing [A] means giving up [X]
- Choosing [B] means giving up [Y]

## Recommendation
[2-3 sentences — take a position]

## What Would Change This
- If [assumption] is wrong → [different winner]
- Key unknown: [thing to investigate]
```

## Design Principles

- **Be opinionated.** Don't sit on the fence. Make a recommendation.
- **Show your work.** Every score needs a rationale, even if brief.
- **Quantify where possible.** "$300K more over 4 years" beats "better comp."
- **Name the tradeoff.** Every choice has a cost. Say what it is.
- **Keep it scannable.** The user should get the answer in 10 seconds from the top, then dig into detail.
