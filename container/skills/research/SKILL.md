---
name: research
description: Deep research on companies, people, and topics using Exa semantic search and Firecrawl content extraction. Use for interview prep, company research, competitive intel, and general investigations.
allowed-tools: Bash(exa-search:*), Bash(firecrawl-scrape:*)
---

# Research Tools

You have two research tools available via bash:

## exa-search — Semantic Search

Finds articles, interviews, blog posts, and discussions by meaning (not just keywords).

```bash
exa-search "query" [num_results] [start_date] [category]
```

**Examples:**
```bash
exa-search "What it's like to work at Anthropic"
exa-search "Anthropic CEO interview about company vision" 5
exa-search "Recent news about Cursor funding" 5 2025-09-01
exa-search "VP Product at AI startups San Francisco" 10 "" company
```

**Best for:**
- Culture and first-hand accounts: "A first-hand account of working at {company}"
- Founder/CEO interviews: "Interview with {company} founder about building the company"
- Business deep dives: "Deep dive analysis of {company} business model and strategy"
- Recent news: Use start_date for last 6 months
- Community discussions: "working at {company} what is it like"
- People research: Use category "company" or "people"

**Tip:** Semantic queries work much better than keyword queries. "A first-hand account of working at Stripe" beats "Stripe employee review".

## firecrawl-scrape — Content Extraction

Extracts clean, readable content from any URL. Use after exa-search finds relevant URLs.

```bash
firecrawl-scrape "url"
```

**Example:**
```bash
firecrawl-scrape "https://techcrunch.com/2026/01/15/company-raises-100m"
```

## Research Workflow (2-Phase Pattern)

For thorough research, follow this pattern:

### Phase 1: Discovery (Exa)
Run multiple semantic queries from different angles:

```bash
# Company research example — run 4-6 queries
exa-search "A first-hand account of what it's like to work at {company}" 5
exa-search "{company} CEO founder interview about company vision" 5
exa-search "Deep dive analysis of {company} business model and strategy" 5
exa-search "Recent news about {company} funding and announcements" 5 2025-09-01
exa-search "Inside {company} company culture and how the team operates" 5
```

### Phase 2: Deep Extraction (Firecrawl)
Take the most promising URLs from Phase 1 and extract full content:

```bash
firecrawl-scrape "https://best-result-1.com/article"
firecrawl-scrape "https://best-result-2.com/interview"
firecrawl-scrape "https://best-result-3.com/deep-dive"
```

### Phase 3: Synthesis (You)
Synthesize all extracted content into an organized briefing covering:
- **Company overview** — what they do, stage, funding
- **Culture** — what it's like to work there, values
- **Leadership** — founders, key execs, vision
- **Strategy** — business model, competitive position
- **Recent developments** — news, launches, funding
- **Key insights** — things that aren't obvious from the website

## Person Research

```bash
exa-search "{person name} interview or podcast or talk" 5
exa-search "{person name} {company} leadership philosophy" 5
exa-search "{person name} career background story" 5
```

Then extract the best URLs with firecrawl-scrape.

## Cost Awareness

Both APIs have per-call billing. Be efficient:
- Use 5 results per query (not 10) for focused research
- Only firecrawl-scrape the most relevant URLs (top 3-5)
- Skip URLs that are clearly low-value from the Exa snippet
