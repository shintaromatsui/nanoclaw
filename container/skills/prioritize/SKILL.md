---
name: prioritize
description: Apply structured prioritization frameworks — RICE, MoSCoW, Value vs Effort, Weighted Scoring. Use when someone says "prioritize these", "RICE score", "MoSCoW", "value vs effort", "rank these features", "stack rank", "what should we build first", "priority matrix", or needs to systematically rank options.
---

# Feature & Initiative Prioritization

Apply structured prioritization frameworks to any list of items. Stop arguing about priority — score it.

## Input

Parse the message to extract:
- **Items to prioritize** (required): List of features, initiatives, tasks, or options
- **Framework** (optional): RICE, MoSCoW, value-effort, weighted (default: RICE)
- **Context** (optional): Business goals, constraints, team size, timeline
- **Criteria** (optional): Custom scoring criteria for weighted scoring

Examples:
- "RICE score these: dark mode, API v2, SSO, mobile app, onboarding redesign"
- "MoSCoW for Q2: [feature list]"
- "value vs effort for these 8 features"
- "prioritize with criteria: revenue impact, customer demand, eng effort, strategic fit"

If items provided without a framework, default to RICE. If fewer than 3 items, suggest a trade-off comparison instead.

## Process

### Step 1: Clarify Items

For each item, ensure enough context to score:
- What does it do? (1-sentence description)
- Who benefits?
- Any known data? (customer requests, revenue impact, effort estimates)

If context is thin, make reasonable assumptions and label clearly.

### Step 2: Apply Framework

#### RICE

Score = (Reach x Impact x Confidence) / Effort

- *Reach:* People/accounts affected per quarter
- *Impact:* 3=Massive, 2=High, 1=Medium, 0.5=Low, 0.25=Minimal
- *Confidence:* 100%=Data-backed, 80%=Some data, 50%=Gut feel
- *Effort:* Person-months total

Format output:

```
*RICE Scorecard*

*SSO* — Score: 1,067 — Rank #1
Reach: 2,000 | Impact: 2 | Confidence: 80% | Effort: 3

*Onboarding* — Score: 625 — Rank #2
Reach: 5,000 | Impact: 1 | Confidence: 50% | Effort: 4

[continue...]
```

#### MoSCoW

Categorize each item with reasoning:

```
*MoSCoW — Q2 2026*

*MUST HAVE* (non-negotiable):
• SSO — Required for 3 enterprise deals worth $800K
• API v2 — Rate limits blocking top 10% of customers

*SHOULD HAVE* (important, not critical):
• Onboarding redesign — 40% trial drop-off at step 3

*COULD HAVE* (nice to have):
• Dark mode — Most-requested community feature

*WON'T HAVE* (this cycle):
• Mobile app — Needs dedicated team (revisit Q4)
```

Rules: Musts ≤ 60% of capacity. Every Must needs a reason.

#### Value vs Effort (2x2)

Score each item: Value (1-10), Effort (1-10). Plot into quadrants:

```
*Value vs Effort Matrix*

*QUICK WINS* (high value, low effort — do first):
• SSO (V:8, E:4)
• Onboarding (V:7, E:5)

*MAJOR PROJECTS* (high value, high effort — plan carefully):
• API v2 (V:9, E:8)

*FILL-INS* (low value, low effort — spare capacity):
• Dark mode (V:3, E:2)

*AVOID* (low value, high effort — not now):
• AI chat (V:4, E:9)
```

#### Weighted Scoring

Custom criteria with weights. Produce scored table and rank.

### Step 3: Synthesize

1. State the recommended priority order
2. Flag conflicts between framework ranking and intuition
3. Identify dependencies (if B depends on A, note it)
4. Recommend tiers:
   - *Tier 1 (commit):* Definitely this cycle
   - *Tier 2 (stretch):* If Tier 1 finishes early
   - *Tier 3 (backlog):* Not this cycle

### Step 4: Persist (Optional)

If the user wants to save, store in `/workspace/group/ops/backlogs/[name].json` with scores, rationale, and date.

## Design Principles

- **Frameworks are tools, not answers.** If the score feels wrong, the inputs are wrong.
- **Make assumptions explicit.** Every score traceable to a reason.
- **Effort is the most lied-about variable.** When in doubt, multiply by 1.5.
- **Dependencies override scores.** A #3 item that unblocks #1 and #2 goes first.
- **The conversation the framework forces is more valuable than the number it produces.**
