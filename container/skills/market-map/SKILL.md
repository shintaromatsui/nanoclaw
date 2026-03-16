---
name: market-map
description: Map a competitive landscape with segments, players, positioning, and whitespace. Use when someone says "map the market", "competitive landscape", "market map", "who are the players", "industry map", "landscape analysis", "who competes with X", or needs to understand a market's structure, key players, and strategic positioning.
---

# Market Map

Map the competitive landscape of a market or category. Identify segments, players, positioning, and where the whitespace is.

## Input

Parse the message to extract:
- **Market or category** (required): What market to map
- **Focus** (optional): Specific angle — "for enterprise buyers", "from an investor lens", "for job search"
- **Known players** (optional): Companies already known about

Examples:
- "map the compliance automation market"
- "market map for product analytics — enterprise focus"
- "who are the players in AI coding tools"
- "competitive landscape for developer tools"

## Research Protocol

Use the research skill (exa-search + firecrawl) if deeper data is needed:

**Wave 1 — Broad landscape:**
- `"[market] competitive landscape 2025 2026"`
- `"[market] market map"`
- `"[market] startups funding"`
- `"[market] vendors comparison"`

**Wave 2 — Depth on key players:**
- For each major player: funding, ARR (if known), positioning, key customers

Check `/workspace/extra/job-search/company-research/` for existing research first.

Keep research focused — 10-15 minutes max. You're mapping, not doing deep dives.

## Process

### Step 1: Define the Market

- **Market definition:** What is this market? (2-3 sentences)
- **Market size:** TAM/SAM if available, or rough estimate
- **Growth drivers:** What's pushing this market forward
- **Key buyer:** Who buys these products and why

### Step 2: Identify Segments

Break the market into 3-6 segments based on how players differentiate:
- By buyer: SMB vs Mid-Market vs Enterprise
- By approach: Platform vs Point Solution vs Open Source
- By use case: [specific to market]

### Step 3: Map the Players

For each segment, list key players. Per player, capture:
- Company name
- One-line positioning
- Stage / funding / valuation (if known)
- Estimated scale (ARR, customers, employees)
- Key differentiator (1 sentence)
- Notable customers

```
## Market Map: [Category]

### Segment 1: [Name]
[What defines this segment. Who buys here.]

- **[Player A]** — [positioning]. [Stage/funding]. [Key differentiator].
- **[Player B]** — [positioning]. [Stage/funding]. [Key differentiator].

### Segment 2: [Name]
[Same structure]
```

### Step 4: Analyze Positioning & Dynamics

- **Category leader(s):** Who's winning and why?
- **Fastest movers:** Who's growing fastest / gaining share?
- **Incumbents at risk:** Who could be disrupted?
- **Emerging threats:** New entrants, open source, platform shifts (AI, etc.)
- **Consolidation signals:** M&A activity, partnerships, convergence

### Step 5: Identify Whitespace

- **Underserved segments:** Who isn't being served well?
- **Positioning gaps:** What positioning isn't claimed by anyone?
- **Emerging needs:** What buyers will want in 12-24 months that nobody offers yet?

## Output Format

```
# Market Map: [Category]

**Date:** [today]
**Market size:** [TAM estimate]
**Growth:** [rate or direction]

## TL;DR
[3-4 sentences: Who's winning, what's changing, where the opportunity is]

## Market Segments

### [Segment 1]: [Name]
[Players with details]

### [Segment 2]: [Name]
[Players with details]

## Competitive Dynamics
- **Leader:** [who and why]
- **Challenger:** [who's coming up]
- **Disruptor:** [what could change everything]

## Whitespace & Opportunities
- [Opportunity 1]
- [Opportunity 2]
- [Opportunity 3]

## Key Trends Shaping This Market
1. [Trend + implication]
2. [Trend + implication]
3. [Trend + implication]

## Sources
[Key sources used]
```

## Design Principles

- **Structure over exhaustiveness.** A clear map of 15 players beats an exhaustive list of 50.
- **Positioning > features.** How companies position themselves matters more than feature checklists.
- **Whitespace is the insight.** Anyone can list players. The value is in seeing what's missing.
- **Recency matters.** Markets shift fast. Prioritize 2025-2026 data over older reports.
- **Connect to Shintaro's context.** If evaluating a company in this market, tie the map back to that decision.
