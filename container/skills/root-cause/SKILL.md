---
name: root-cause
description: Systematic diagnosis from symptom to root cause using 5 Whys and Fishbone analysis. Use when someone says "why is this happening", "root cause", "diagnose", "what went wrong", "5 whys", "fishbone", "what is causing", "troubleshoot", "post-mortem", or needs to move from symptoms to the real underlying problem.
---

# Root Cause Analysis

Stop treating symptoms. Find the actual cause. Uses 5 Whys to drill down and Fishbone (Ishikawa) to map out all possible causes systematically.

## Input

Parse the message to extract:
- **Problem or symptom** (required): What's going wrong
- **Context** (optional): What's already been tried, when it started, who's affected
- **Depth** (optional): Quick (5 Whys only) or Full (5 Whys + Fishbone + recommendations)

Examples:
- "root cause: our enterprise close rate dropped from 35% to 20%"
- "why can't we hire senior engineers fast enough — do a 5 whys"
- "post-mortem: customer onboarding takes 3x longer than it should"
- "why do I keep procrastinating on this project"

## Process

### Step 1: Define the Problem Precisely

Restate the problem with specifics:
- **What** is happening (vs what should be happening)?
- **When** did it start?
- **Where** does it occur (segment, geography, team, product area)?
- **How big** is the gap? Quantify if possible.

Bad: "Retention is bad"
Good: "30-day retention for enterprise accounts dropped from 92% to 84% between Q3 and Q4 2025"

### Step 2: The 5 Whys

Start from the symptom and ask "why?" at each level:

```
Symptom: [The problem as stated]
↓ Why?
Why 1: [First-level cause — usually obvious]
↓ Why?
Why 2: [Deeper — getting past the surface]
↓ Why?
Why 3: [Now we're in systems/process territory]
↓ Why?
Why 4: [Organizational or structural cause]
↓ Why?
Why 5: [Root cause — the thing that, if fixed, prevents recurrence]
```

**Rules:**
- Each "why" must be a factual cause, not a guess. Flag hypotheses clearly.
- If a "why" has multiple valid answers, branch the tree.
- Stop when you reach something actionable and systemic.
- Avoid blame. "There was no process ensuring X got done" not "John didn't do X."

### Step 3: Fishbone Diagram (Full mode)

Map ALL possible causes across standard categories:

```
                                    ┌─ [Cause] ─ [Sub-cause]
                    ┌── People ─────┤
                    │               └─ [Cause]
                    ├── Process ────┤─ [Cause]
Problem ────────────┤               └─ [Cause]
                    ├── Technology ─┤─ [Cause]
                    │               └─ [Cause]
                    ├── Data ───────┤─ [Cause]
                    └── External ───┤─ [Cause]
```

**Categories:**
- **People:** Skills, capacity, motivation, communication, turnover
- **Process:** Workflow gaps, handoffs, unclear ownership, missing steps
- **Technology:** Tools, infrastructure, integration failures, technical debt
- **Data:** Missing data, bad data, delayed data, wrong metrics
- **External:** Market shifts, customer behavior changes, competitive moves

For each cause, rate:
- **Likelihood:** High / Medium / Low
- **Evidence:** Data / Anecdote / Hypothesis

### Step 4: Converge on Root Cause(s)

Identify the 1-3 most likely root causes. For each:
- **Evidence for:** What supports this?
- **Evidence against:** What contradicts it?
- **Test:** How would you confirm or rule this out?
- **If true, fix is:** What would you do about it?

### Step 5: Recommend Actions

For the top root cause(s):

**Immediate (this week):** What stops the bleeding right now?
**Structural (this quarter):** What prevents recurrence?
**Systemic (ongoing):** What detection mechanism ensures you catch this earlier next time?

## Output Format

```
# Root Cause Analysis: [Problem]

**Problem:** [precise problem statement with numbers]

## 5 Whys

Symptom: [problem]
↓ Why 1: [cause]
↓ Why 2: [cause]
↓ Why 3: [cause]
↓ Why 4: [cause]
↓ Why 5: [ROOT CAUSE]

## Root Cause Verdict

**Primary:** [Root cause #1] — Confidence: [High/Medium/Low]
- Evidence: [what supports this]
- Test: [how to confirm]

**Contributing:** [Root cause #2, if applicable]

## Recommended Actions

**Stop the bleeding (this week):**
- [Action 1]
- [Action 2]

**Fix the system (this quarter):**
- [Action 1]

**Early warning (ongoing):**
- [What to monitor so you catch this faster next time]
```

## Design Principles

- **No blame, only systems.** "The system allowed X to fail" not "Person X failed."
- **Evidence over intuition.** Label every cause as Data / Anecdote / Hypothesis.
- **The root cause is actionable.** If you can't do anything about it, go one level up.
- **Multiple causes are normal.** Most real problems have 2-3 contributing causes.
- **The early warning is the most valuable output.** Finding the cause is good. Building the alarm system is better.
