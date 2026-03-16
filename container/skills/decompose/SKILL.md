---
name: decompose
description: Break any problem into a MECE issue tree with prioritized components. Use when someone says "break this down", "decompose", "issue tree", "structure this problem", "MECE", "how do I think about this", "unpack this", or needs to turn a vague or complex problem into an organized, actionable structure.
---

# Problem Decomposition

Break any messy, complex problem into a structured MECE (Mutually Exclusive, Collectively Exhaustive) issue tree. Turn "I don't know where to start" into "here are the 4 things that matter."

## Input

Parse the message to extract:
- **Problem or question** (required): What to decompose
- **Depth** (optional): How many levels deep (default: 3)
- **Lens** (optional): Specific perspective — "from an investor lens", "as a product leader", "for board presentation"

Examples:
- "decompose why our retention is dropping"
- "break down how I should evaluate this job offer"
- "MECE the levers for revenue growth at a $50M ARR SaaS"
- "unpack what's causing slow hiring — from an ops lens"

## Process

### Step 1: Clarify the Root Question

Restate the problem as a single, clear question:
- Bad: "Revenue is a problem"
- Good: "What are the levers to accelerate revenue growth from $50M to $100M ARR?"

### Step 2: Choose the Decomposition Framework

Pick the right framework based on the problem type:

**Revenue/Growth problems:**
- Revenue = Customers × ARPU
- Customers = New + Existing - Churned
- Growth = Acquisition + Expansion - Contraction - Churn

**Operational problems:**
- Process: Inputs → Activities → Outputs → Outcomes
- Bottleneck analysis: where does flow break?

**Strategic decisions:**
- Options × Evaluation criteria (weighted)
- Time horizons: Now / Next / Later

**Diagnostic problems (why is X happening?):**
- Hypothesis tree: list possible causes, then sub-causes
- Internal vs External factors
- People / Process / Technology / Data

**Career/Personal decisions:**
- Financial / Career capital / Lifestyle / Risk dimensions
- Short-term vs Long-term tradeoffs

### Step 3: Build the Tree

Decompose to 3 levels (or user-specified depth):

```
Root Question
├── Branch 1: [Component]
│   ├── Sub-branch 1a
│   │   ├── Leaf 1a-i
│   │   └── Leaf 1a-ii
│   └── Sub-branch 1b
├── Branch 2: [Component]
│   ├── Sub-branch 2a
│   └── Sub-branch 2b
└── Branch 3: [Component]
    ├── Sub-branch 3a
    └── Sub-branch 3b
```

**MECE check at every level:**
- **Mutually Exclusive:** No overlap between branches
- **Collectively Exhaustive:** Nothing important is missing

### Step 4: Prioritize

For each Level 1 branch, assess:
- **Impact:** High / Medium / Low
- **Certainty:** High / Medium / Low
- **Actionability:** High / Medium / Low

Mark the 1-2 branches that are highest leverage.

### Step 5: Identify Key Questions

For each high-priority branch, name the 1-2 questions that would resolve it:
- What data would tell us whether this is the real driver?
- What experiment would test this?
- Who would know the answer?

## Output Format

```
# Decomposition: [Root Question]

**Framework:** [which framework and why]

## The Tree

[ASCII tree]

## Branch Analysis

### Branch 1: [Name] — [Impact: High/Med/Low]
[2-3 sentences on what this branch covers and why it matters]
**Key question:** [The one thing to resolve]
**Data needed:** [What would answer it]

### Branch 2: [Name] — [Impact: High/Med/Low]
[Same structure]

### Branch 3: [Name] — [Impact: High/Med/Low]
[Same structure]

## Priority Call

**Start here:** [Which branch to attack first and why]
**Ignore for now:** [Which branch is low-leverage and why]

## MECE Check
- **Gaps:** [Anything potentially missing?]
- **Overlaps:** [Any branches that bleed into each other?]
```

## Design Principles

- **MECE is the standard.** If the tree isn't MECE, it's not a decomposition — it's a brainstorm.
- **3 levels is usually enough.** Going deeper often means you're solving, not structuring.
- **Prioritize ruthlessly.** A 12-branch tree with no prioritization is worse than a 4-branch tree with clear "start here."
- **Name the framework.** Being explicit about which decomposition lens you're using makes the structure auditable.
