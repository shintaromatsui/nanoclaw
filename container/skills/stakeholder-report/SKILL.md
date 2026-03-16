---
name: stakeholder-report
description: Generate audience-tailored reports — same data, different framing for board, engineering, sales, support, or executive audiences. Use when someone says "send update to", "board update", "investor update", "team update", "status report for", "stakeholder update", "report for engineering", "update sales team", or needs to communicate information to different audiences.
---

# Stakeholder Report Generator

Same data, different framing. Generate reports tailored to what each audience cares about.

## Input

Parse the message to extract:
- **Audience** (required): board, investors, engineering, sales, support, executive, or custom
- **Topic or data** (required): What the report covers
- **Source** (optional): File paths in `/workspace/group/`, KPI tracker data, or context

Examples:
- "board update on Q1 performance"
- "engineering update on API v2"
- "sales update on upcoming features"
- "support update on known issues"
- "investor update using KPI data"

## Process

### Step 1: Gather Data

Check for relevant data in:
- `/workspace/group/ops/metrics/` — KPI tracker
- `/workspace/group/ops/launches/` — Launch readiness
- `/workspace/group/ops/roadmaps/` — Roadmap data
- User-provided context

### Step 2: Apply Audience Template

#### Board / Investors

What they care about: Are we winning? Where's the risk? What do you need?

```
*Board Update: [Period]*

*Headline:* [1 sentence]

*Key Metrics*
• ARR: $X.XM vs target $X.XM [status]
• Net New ARR: $XXK [status]
• Customers: XXX [status]
• NRR: XXX% [status]
• Runway: XX months [status]

*Strategic Progress*
• [Initiative 1]: [status] — [impact]
• [Initiative 2]: [status] — [impact]

*Risks*
• [Risk 1] — Likelihood: [H/M/L] — Mitigation: [action]

*Asks*
1. [Decision needed] — by [date]
```

#### Engineering

What they care about: Technical status, blockers, decisions needed.

```
*Engineering Update: [Period/Project]*

*Summary:* [2-3 sentences]

*[Project 1]* — [ON TRACK / AT RISK / BLOCKED]
Shipped: [what completed]
In progress: [what's active]
Blocked: [what's stuck]
Next: [milestones]

*Velocity*
Points completed: XX (vs XX avg)
Bugs: XX resolved, XX new (net: [+/-])

*Decisions Needed*
1. [Decision] — Options: [A, B] — Recommend: [X] — By: [date]

*Dependencies*
Waiting on [team] for [thing] — expected [date]
```

#### Sales

What they care about: What can I sell? When? How do we beat competitors?

```
*Sales Update: [Period]*

*Available now:*
• [Feature] — [benefit] | [which tiers]

*Coming this quarter:*
• [Feature] (month) — [benefit]

*Competitive intel:*
• [Competitor]: [what they did] — Our response: [positioning]

*Talk tracks:*
• When asked about [topic]: "[response]"

*Do NOT promise:*
• [Feature/timeline not committed]
```

#### Support

What they care about: What's broken? Workaround? When fixed?

```
*Support Update: [Period]*

*Active Known Issues*

*[Issue 1]* — Severity: [level]
Symptoms: [what customer sees]
Workaround: [what to tell them]
Fix ETA: [date]
Affected: [scope]

*Recently Resolved*
• [Issue] — fixed [date]

*Upcoming Changes (may generate tickets)*
• [Change] on [date] — Expect: [ticket impact]

*Escalation*
• [Issue type] → [team/person] via [channel]
```

#### Executive

Pyramid principle: conclusion first, evidence below.

```
*[Topic]: Executive Summary*

*Bottom line:* [2-3 sentences — the answer. Stop here if busy.]

*Evidence:*
• [Point 1 with data]
• [Point 2 with data]
• [Point 3 with data]

*Risks:* [risk] — Mitigation: [action]

*Decision needed:* [what to decide, with options]

*Next steps:*
1. [Action] — [owner] — [date]
```

### Step 3: Deliver

Send via send_message. Offer to also draft as email or save as Google Doc.

## Design Principles

- **Audience determines framing, not content.** Facts don't change. Emphasis and language do.
- **Board wants metrics. Engineering wants status. Sales wants features. Support wants issues.**
- **Pyramid principle for executives.** Conclusion first. They stop reading when they have enough.
- **Include what NOT to say.** Especially for sales and support — guardrails prevent miscommunication.
- **Action items are non-negotiable.** Every report ends with clear next steps.
