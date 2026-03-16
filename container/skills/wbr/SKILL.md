---
name: wbr
description: Generate a comprehensive Weekly Business Review synthesizing metrics, competitive intel, and operational status. Use when someone says "weekly business review", "WBR", "business review", "weekly review", "weekly ops review", "how did the week go", or needs a structured multi-section business review.
---

# Weekly Business Review (WBR)

Comprehensive weekly business review. Synthesizes metrics, competitive intel, and operational status into a structured review.

## Input

Parse the message to extract:
- **Company or business** (optional): What to review (default: use available data)
- **Period** (optional): Which week (default: most recent)
- **Focus areas** (optional): Sections to emphasize
- **Data sources** (optional): File paths or context

Examples:
- "WBR"
- "weekly business review for Acme Corp"
- "WBR focus on revenue and customers"
- "business review using KPI data"

## Process

### Step 1: Gather Data

Pull from available sources:
- `/workspace/group/ops/metrics/` — KPI tracker data
- `/workspace/group/ops/roadmaps/` — Product roadmap status
- `/workspace/group/ops/launches/` — Launch readiness
- User-provided data
- Web research for competitive activity (Exa/Firecrawl if needed)

If data is sparse, label what's available vs. estimated vs. missing. A WBR with gaps and clear labels beats fabricated numbers.

### Step 2: Build the WBR

```
*Weekly Business Review*
Week of [date range]

━━━━━━━━━━━━━━━━━━━

*1. Executive Summary*

This week in 5 bullets:
• [Most important metric/milestone/event]
• [Second most important]
• [Third]
• [Key risk or concern]
• [Looking ahead]

Overall: 🟢/🟡/🔴

━━━━━━━━━━━━━━━━━━━

*2. Key Metrics*

• MRR: $XXK (+X.X% WoW) vs $XXK target 🟢
• New Customers: XX (+XX%) vs XX target 🟡
• Churn: X.X% vs <X% target 🟢
• NPS: XX vs >XX target 🔴
• Active Users: X,XXX (+X.X% WoW) 🟢
• Pipeline: $X.XM vs $X.XM target 🟡

Alerts:
🔴 [RED metrics with context]
🟡 [YELLOW metrics trending wrong]

━━━━━━━━━━━━━━━━━━━

*3. Revenue*

MRR: $XXK (+X.X% WoW, +XX% MoM)
• New: $XXK from XX customers
• Expansion: $XXK from XX accounts
• Churned: -$XXK from XX accounts
• Net new: $XXK

Run rate: $X.XM ARR
vs Plan: [ahead/behind] by [amount]

Notable:
• Won: [Customer] $XXK — [context]
• Lost: [Customer] $XXK — [reason]

━━━━━━━━━━━━━━━━━━━

*4. Customers*

Acquisition: XX signups (vs XX last week)
Conversion: XX% (vs XX% target)
Churn: X.X% (vs X.X% target)
At-risk: XX accounts

━━━━━━━━━━━━━━━━━━━

*5. Pipeline*

Total: $X.XM (vs $X.XM target)
Created this week: $XXK
Velocity: $XXK/week (need $XXK/week)

Stages:
• Discovery: $XXK (XX deals)
• Evaluation: $XXK (XX deals)
• Negotiation: $XXK (XX deals)
• Closing: $XXK (XX deals)

━━━━━━━━━━━━━━━━━━━

*6. Product & Engineering*

Shipped:
• [Feature/fix] — [impact]
• [Feature/fix] — [impact]

In progress:
• [Project] — [on track/at risk] — ETA: [date]

Velocity: XX points (vs XX committed)
Bugs: XX resolved, XX new

━━━━━━━━━━━━━━━━━━━

*7. Competitive*

• [Competitor A]: [what they did]
  Our take: [assessment]
• [Competitor B]: [what they did]
  Our take: [assessment]

Win/loss: Won XX vs [competitor], Lost XX to [competitor]

━━━━━━━━━━━━━━━━━━━

*8. Risks*

🔴 [Risk 1] — Owner: [name] — [mitigation]
🟡 [Risk 2] — Owner: [name] — [mitigation]

New: [risk identified this week]
Resolved: [risk mitigated]

━━━━━━━━━━━━━━━━━━━

*9. Last Week's Actions*

✅ [Action] — [owner] — DONE
⏳ [Action] — [owner] — IN PROGRESS
❌ [Action] — [owner] — NOT STARTED

Completion: X/X (XX%)

━━━━━━━━━━━━━━━━━━━

*10. This Week's Actions*

1. [Most important] — [owner] — [due]
2. [Second] — [owner] — [due]
3. [Third] — [owner] — [due]
```

### Step 3: Quick-Scan Version

Also provide a condensed version:

```
*WBR Quick Scan — Week of [dates]*

Status: 🟡
Wins: [top 2-3]
Concerns: [top 2-3]
Actions: [top 3]
```

## Scheduling

To set up weekly WBR generation, use `mcp__nanoclaw__schedule_task` with:
- schedule_type: "cron"
- schedule_value: "0 9 * * 1" (Monday 9am)
- context_mode: "group"
- prompt: "Generate the weekly business review using latest KPI data"

## Design Principles

- **Consistent structure every week.** People know where to find things.
- **Traffic lights everywhere.** Scannable in 10 seconds.
- **Action items are the most important section.** Everything else is context.
- **Last week's actions get graded.** Accountability requires tracking.
- **Competitive section is mandatory.** If nothing happened, say so.
- **Data gaps are labeled, not filled.** "Not available" beats a made-up number.
- **The 5-bullet executive summary is the most-read section.** Get it right.
