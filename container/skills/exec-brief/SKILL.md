---
name: exec-brief
description: Distill messy information into a structured 1-page executive brief. Use when someone says "exec brief", "executive summary", "one pager", "distill this", "brief me on", "turn this into a brief", "make this crisp", or needs to synthesize research, notes, or data into a concise decision-ready document.
---

# Executive Brief

Turn chaos into a crisp, 1-page executive brief. This is the "so what?" document.

## Input

Parse the message to extract:
- **Topic** (required): What the brief is about
- **Source material** (optional): Pasted content, file paths, or context to synthesize
- **Audience** (optional): Who will read this (default: Shintaro or exec team)
- **Decision needed** (optional): What action this brief should drive

Examples:
- "exec brief on Vanta opportunity"
- "make this a one pager" (then paste notes)
- "brief me on the compliance market for a board deck"

## Process

### Step 1: Gather Source Material

Check these locations for existing context:
- `/workspace/extra/job-search/company-research/` — company research
- `/workspace/group/intelligence.md` — prior context and learnings
- Any content pasted directly in the message

If topic-only (no pasted content), check for existing research before doing new research.

### Step 2: Extract the Signal

From all source material, identify:
1. **The core question or situation** — What is this about? (1 sentence)
2. **3 key findings** — The most important things to know (hard limit: 3)
3. **Implications** — What do the findings mean for the reader?
4. **Recommended action** — What should happen next?
5. **Risks** — What could go wrong?

Ruthlessly cut. If a finding doesn't change the recommendation, it doesn't belong.

### Step 3: Write the Brief

```
# [Title]: Executive Brief

**Date:** [today]
**Prepared for:** [audience]

---

## Situation
[2-3 sentences. What's happening, why it matters, what prompted this brief.]

## Key Findings

1. **[Finding 1 headline]**
   [2-3 sentences with specific data points. No vague claims.]

2. **[Finding 2 headline]**
   [2-3 sentences with specific data points.]

3. **[Finding 3 headline]**
   [2-3 sentences with specific data points.]

## Implications
[2-3 bullet points. Connect findings to what the reader cares about.]

## Recommended Action
[1-2 sentences. Be specific and direct. "We should X by Y because Z."]

## Risks & Mitigations
- **[Risk 1]** — [Mitigation]
- **[Risk 2]** — [Mitigation]

## Key Assumptions
[Bullet list of things this analysis assumes to be true.]
```

### Step 4: Quality Check

Before delivering, verify:
- Can someone get the answer in 30 seconds by reading Situation + Recommended Action?
- Are all 3 findings supported by specific evidence (numbers, quotes, data)?
- Is the recommendation actionable (not "we should think about...")?
- Would this fit on one printed page?

If the brief is longer than ~400 words in the body, cut more.

## Design Principles

- **One page, period.** If it doesn't fit, you haven't synthesized enough.
- **Findings ≤ 3.** If you have 5 findings, two of them aren't important enough.
- **Specific > vague.** "$300M ARR growing 100% YoY" not "strong growth."
- **Recommendation is mandatory.** Don't present without a position.
- **Lead with the answer.** Situation + Recommended Action should be readable standalone.
- **Write in Shintaro's voice.** Direct, no jargon, short paragraphs.
