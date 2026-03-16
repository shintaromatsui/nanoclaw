---
name: thesis
description: Build the case for AND against a hypothesis with structured evidence and a verdict. Use when someone says "build a case for", "should I do X", "what is the case for", "thesis on", "argue for and against", "devil's advocate", "make the argument", or needs structured thinking on a big decision, bet, or strategic question.
---

# Thesis Builder

Build a rigorous, balanced case for AND against a hypothesis. This isn't a pros/cons list — it's structured argumentation with evidence, confidence levels, and a verdict.

## Input

Parse the message to extract:
- **Hypothesis** (required): The claim or decision to evaluate
- **Context** (optional): Background, constraints, stakes
- **Lean** (optional): If already leaning a direction, noted — then steelman the other side harder

Examples:
- "thesis: I should take the Vanta VP role over staying at Amplitude"
- "build the case for Vanta IPO within 18 months"
- "should we build vs buy for compliance tooling — argue both sides"
- "is the compliance market winner-take-all"

## Process

### Step 1: Sharpen the Hypothesis

Restate as a falsifiable claim:
- Bad: "Vanta is a good company"
- Good: "Joining Vanta as VP will generate more career capital and financial upside over 4 years than staying at Amplitude"

### Step 2: Gather Evidence

Check existing research:
- `/workspace/extra/job-search/company-research/` for company-specific data
- `/workspace/group/intelligence.md` for prior context
- Use the research skill (Exa + Firecrawl) for fresh data if needed

Don't over-research — 15 minutes of targeted searching, not a PhD.

### Step 3: Build the Evidence Matrix

For EACH side, find 3-5 pieces of evidence:

**Case FOR (Bull Case):**
For each piece:
- **Claim:** What it supports (1 sentence)
- **Evidence:** Specific data, quote, or fact
- **Strength:** Strong / Moderate / Weak
- **Source:** Where this comes from

**Case AGAINST (Bear Case):**
Same structure. Must be at least as thorough as the bull case. If leaning FOR, work harder on the bear side — that's where the value is.

### Step 4: Assess Key Unknowns

List 3-5 things that, if known, would decisively resolve the question:
- What data would make you confident FOR?
- What data would make you confident AGAINST?
- Can any of these be resolved? How?

### Step 5: Deliver Verdict

Include a pre-mortem if verdict is FOR:
> "It's 12 months later and this was the wrong call. What happened?"
> [2-3 most likely failure modes]

## Output Format

```
# Thesis: [Hypothesis]

**Verdict:** [FOR / AGAINST / CONDITIONAL]
**Confidence:** [High / Medium / Low] — [1 sentence on why]

---

## The Case FOR

### 1. [Claim headline]
[Evidence + source. 2-3 sentences.]
**Strength:** Strong / Moderate / Weak

### 2. [Claim headline]
[Evidence + source.]
**Strength:** Strong / Moderate / Weak

### 3. [Claim headline]
[Evidence + source.]
**Strength:** Strong / Moderate / Weak

## The Case AGAINST

### 1. [Claim headline]
[Evidence + source.]
**Strength:** Strong / Moderate / Weak

### 2. [Claim headline]
[Evidence + source.]
**Strength:** Strong / Moderate / Weak

### 3. [Claim headline]
[Evidence + source.]
**Strength:** Strong / Moderate / Weak

## Key Unknowns
- [Unknown 1] — How to resolve: [method]
- [Unknown 2] — How to resolve: [method]

## Verdict

**[FOR / AGAINST / CONDITIONAL]** at **[High / Medium / Low]** confidence.

[2-3 sentences explaining the reasoning. Name the single strongest argument on each side.]

**If this assumption is wrong, flip the verdict:** [The one thing that would change everything]

## Pre-mortem (if FOR)
It's 12 months later and this was wrong. What happened?
- [Failure mode 1]
- [Failure mode 2]
- [Failure mode 3]
```

## Design Principles

- **Steelman both sides.** The value is in the best version of the argument you disagree with.
- **Evidence over opinion.** Every claim needs a fact, number, or credible source.
- **Name your confidence.** "Medium confidence because [specific reason]" not "I think."
- **One verdict.** Don't hedge with "it depends." If conditional, name the exact condition.
- **The pre-mortem is the most valuable part.** It surfaces risks that optimism hides.
