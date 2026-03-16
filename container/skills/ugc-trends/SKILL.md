# UGC Trends — TikTok Trend Intelligence

Pulls trending TikTok content in a given niche and surfaces what's working: top videos, viral formats, engagement patterns, and content gaps.

## Trigger phrases
"what's trending", "ugc trends", "what's working on tiktok", "trending in [niche]", "viral content", "what should I post", "content ideas for", "what format is working"

## Tools needed
- Bash (for Apify API calls via Node.js)
- send_message (to deliver results)

## Process

### Step 1: Parse the request
Extract:
- **Niche/topic** (required) — e.g. "Tokyo coffee", "specialty coffee Japan", "travel Tokyo"
- **Hashtags to search** (derive from niche if not given)
- **Goal** — trend scan, content ideas, or competitor analysis

### Step 2: Run Apify TikTok Scraper

Use the Apify API with key from environment variable `APIFY_API_KEY`.

**Start a run:**
```
POST https://api.apify.com/v2/acts/clockworks~tiktok-scraper/runs
Authorization: Bearer {APIFY_API_KEY}
Content-Type: application/json

{
  "hashtags": ["tokyocoffee", "tokyocafe", "specialtycoffee"],
  "resultsPerPage": 20,
  "maxItems": 20
}
```

**Poll until complete** (check every 5 seconds):
```
GET https://api.apify.com/v2/actor-runs/{runId}
```
When `status === "SUCCEEDED"`, get `defaultDatasetId`.

**Fetch results:**
```
GET https://api.apify.com/v2/datasets/{datasetId}/items?limit=20
```

Use Node.js with the `https` module (no external packages needed).

### Step 3: Analyze the data

For each video, extract:
- `text` — description/caption
- `diggCount` — likes
- `playCount` — views
- `shareCount` — shares
- `commentCount` — comments
- `authorMeta.name` — creator
- `webVideoUrl` — URL

**Sort by shareCount** (shares = viral signal, not just passive views).

**Identify patterns:**
- What hooks appear in high-share captions?
- What video lengths correlate with high completion (if available)?
- Which creators dominate the niche?
- What content angles are missing (gaps)?

**Engagement formula for scoring:**
`score = (shares × 3) + (likes × 1) + (comments × 2)`
Shares weighted highest — they signal content worth spreading.

### Step 4: Output format

Send via send_message:

```
📊 *TikTok Trends — [Niche]*

*Top 3 viral videos right now:*

1. @[creator] — [views]K views · [shares] shares
"[first 80 chars of caption]"
→ Why it works: [one insight]
[url]

2. @[creator] — [views]K views · [shares] shares
"[caption excerpt]"
→ Why it works: [one insight]
[url]

3. @[creator] — [views]K views · [shares] shares
"[caption excerpt]"
→ Why it works: [one insight]
[url]

*What's working (patterns):*
• [Pattern 1 — hook style, format, angle]
• [Pattern 2]
• [Pattern 3]

*Content gaps (what nobody's doing):*
• [Gap 1]
• [Gap 2]

*3 content ideas for you:*
1. [Specific idea based on what's viral + your product]
2. [Specific idea]
3. [Specific idea]
```

## Design principles
- Shares > likes. Shares are the real viral signal.
- Always tie insights back to Shintaro's specific product (Tokyo coffee map, $9 Gumroad)
- Content gaps are as valuable as what's working — that's the whitespace
- Give specific, actionable content ideas — not vague suggestions
