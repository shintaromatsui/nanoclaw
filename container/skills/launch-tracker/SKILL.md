---
name: launch-tracker
description: Multi-functional launch readiness management with persistent tracking and go/no-go decisions. Use when someone says "launch checklist", "launch readiness", "are we ready to launch", "launch status", "go no-go", "launch plan", "ready to ship", "release readiness", or needs to track launch readiness across functions.
---

# Launch Readiness Tracker

Coordinate all functions for a launch. Track readiness across product, engineering, GTM, operations, and systems. Persistent — stores state as JSON.

## Input

Parse the message to extract the **action** and **parameters**:

- **create** `[feature name]` — Initialize a new launch tracker
- **update** `[feature] [category].[item]=[status]` — Update an item
- **status** `[feature]` — Show readiness dashboard
- **blocker** `[feature] [description] owner=[name] due=[date]` — Add a blocker
- **resolve** `[feature] [blocker]` — Mark blocker resolved
- **go-no-go** `[feature]` — Generate go/no-go recommendation
- **list** — Show all active launches

Examples:
- "create launch tracker for SSO"
- "update SSO product.feature_complete=done"
- "SSO launch status"
- "blocker on SSO: legal review of data residency, owner=Legal, due March 20"
- "are we ready to launch SSO"

## Data Storage

Store in `/workspace/group/ops/launches/{feature-slug}.json`:

```json
{
  "name": "SSO Feature",
  "slug": "sso-feature",
  "created": "2026-03-14",
  "target_launch": "2026-04-01",
  "status": "in_progress",
  "categories": {
    "product": {
      "feature_complete": {"status": "done", "updated": "2026-03-14"},
      "tested": {"status": "in_progress", "updated": "2026-03-14"},
      "documented": {"status": "not_started", "updated": "2026-03-14"},
      "accessibility": {"status": "not_started", "updated": "2026-03-14"},
      "security_review": {"status": "not_started", "updated": "2026-03-14"}
    }
  },
  "blockers": [],
  "history": []
}
```

Create `/workspace/group/ops/launches/` on first use if it doesn't exist.

## Process

### Action: create

Initialize with default checklist:

*Product:* feature complete, QA tested, documentation, accessibility, security review
*Engineering:* performance tested, monitoring, rollback plan, feature flags, capacity, migrations
*GTM:* messaging, sales enablement, pricing, marketing assets, launch timing
*Operations:* support trained, FAQ, escalation paths, billing, SLA review
*Systems:* analytics, alerting, runbook, integration testing, data pipeline

### Action: status

```
*Launch Readiness: [Feature]*
Target: [date] | Days left: [X]
Overall: 🔴 NOT READY

*Product* 3/5 🟡
✅ Feature complete
✅ QA tested
✅ Documentation
⏳ Accessibility — in progress
🚫 Security review — BLOCKED

*Engineering* 5/6 🟡
✅ Performance tested
✅ Monitoring
✅ Rollback plan
✅ Feature flags
✅ Capacity
⏳ Migration tested — in progress

*GTM* 1/5 🔴
✅ Messaging
❌ Sales enablement
🚫 Pricing — BLOCKED
🚫 Marketing assets — BLOCKED
❌ Launch timing

*Operations* 2/5 🔴
✅ Support trained
✅ FAQ created
❌ Escalation paths
❌ Billing
❌ SLA review

*Systems* 4/5 🟡
✅ Analytics
✅ Alerting
✅ Runbook
✅ Integration tested
⏳ Data pipeline — in progress

*Blockers*
🚫 Security review — Owner: Legal — Due: Mar 20 — ⚠️ AT RISK
🚫 Pricing approval — Owner: Finance — Due: Mar 18 — ⚠️ AT RISK
🚫 Marketing assets — Owner: Design — Due: Mar 22 — ✅ ON TRACK
```

### Action: go-no-go

```
*Go/No-Go: [Feature]*
Target: [date] | Assessment: [today]

*Recommendation:* 🔴 NO-GO

*Category Assessment*
🟢 Product — GO
🟡 Engineering — GO (migration test pending, low risk)
🔴 GTM — NO-GO (missing sales enablement, pricing)
🟢 Operations — GO
🟢 Systems — GO

*Open Blockers*
[List with impact]

*Conditions for GO:*
1. Pricing approved by [date]
2. Sales enablement complete by [date]

*If NO-GO — New Target:* [date]
Rationale: [why]
```

## Chaining

- Suggest creating runbooks via process-doc for launch operations
- Suggest stakeholder-report for launch communications
- Suggest kpi-tracker for post-launch metric tracking

## Design Principles

- **Cross-functional by default.** Engineering done ≠ ready to launch.
- **Blockers are first-class citizens.** Tracked prominently with owners and dates.
- **Traffic lights are binary.** GREEN = ready. Everything else = not ready.
- **Go/no-go is a recommendation, not a decree.** Present data for the decision maker.
- **Persistent tracking is the point.** Value comes from updating over time.
