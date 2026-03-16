---
name: roadmap
description: Create, maintain, and communicate product roadmaps with audience-specific views. Use when someone says "create a roadmap", "roadmap status", "update the roadmap", "what's on the roadmap", "roadmap for engineering", "roadmap for sales", "what are we building", or needs to manage or communicate a product roadmap.
---

# Product Roadmap Manager

Create, maintain, and communicate product roadmaps. Same data, different views per audience.

## Input

Parse the message to extract the **action** and **parameters**:

- **create** `[roadmap name]` — Initialize a new roadmap
- **add** `[roadmap] [initiative] theme=[theme] timeframe=[now/next/later] team=[team] priority=[P0/P1/P2]`
- **update** `[roadmap] [initiative] status=[status]`
- **view** `[roadmap]` — Now/Next/Later view
- **view** `[roadmap] for [audience]` — Audience-tailored view
- **dependencies** `[roadmap]` — Dependency map

Examples:
- "create Q2 product roadmap"
- "add SSO to roadmap, theme=Enterprise, timeframe=now, P0"
- "roadmap status"
- "show roadmap for sales"
- "show roadmap for leadership"
- "roadmap dependencies"

## Data Storage

Store in `/workspace/group/ops/roadmaps/{name-slug}.json`:

```json
{
  "name": "Q2 2026",
  "initiatives": [
    {
      "name": "SSO",
      "description": "SAML/OIDC single sign-on",
      "theme": "Enterprise",
      "timeframe": "now",
      "status": "in_progress",
      "priority": "P0",
      "team": "Platform",
      "customer_impact": "Unblocks 3 enterprise deals ($800K)",
      "business_impact": "Enables upmarket motion",
      "dependencies": ["Identity service migration"],
      "risks": ["Auth middleware delay"]
    }
  ]
}
```

Create `/workspace/group/ops/roadmaps/` on first use.

Valid statuses: `planned`, `in_progress`, `at_risk`, `completed`, `cut`, `deferred`

## Process

### Default View (Now/Next/Later)

```
*Product Roadmap: [Name]*
Updated: [date]

*NOW — In Progress*

[P0] *SSO* — Platform
Status: IN PROGRESS (on track)
Target: Apr 15
Impact: Unblocks 3 enterprise deals ($800K)

[P0] *API v2* — API team
Status: IN PROGRESS (⚠️ at risk)
Target: May 1
Risk: Schema migration complexity

*NEXT — Planned*

[P1] *Onboarding Redesign* — Growth
Impact: Address 40% trial drop-off
Depends on: SSO (enterprise flow)

*LATER — Future*

[P2] *Mobile App* — TBD
Note: Requires mobile team (hiring Q3)

*Summary*
Now: 4 items (3 on track, 1 at risk)
Next: 3 items
Later: 2 items
```

### View for Engineering

```
*Engineering Roadmap*

*SSO* [P0] — Platform (3 eng, 6 weeks)
Tech: SAML 2.0 + OIDC, identity service integration
Dependencies: Identity migration (DONE), Auth refactor (IN PROGRESS)
Risks: Auth refactor behind by 1 week
Decision needed: Token storage approach

*API v2* [P0] — API (4 eng, 8 weeks)
Tech: REST→GraphQL, new rate limiting, versioned schemas
Risks: Schema migration — considering phased rollout
Decision needed: v1 deprecation policy

*Capacity*
Platform: 5 eng → SSO (3), Billing (2)
API: 4 eng → API v2 (4)
Growth: 3 eng → available after Apr 15
```

### View for Sales

```
*Sales Roadmap*

*Available Now:*
[none new this quarter]

*Coming Soon:*

*SSO (April)* — Enterprise SSO with SAML/OIDC
Talk track: "Enterprise-grade single sign-on"
Competitive: Closes gap with [competitor]
Deal impact: Unblocks [customer A], [customer B]
Pricing: Enterprise tier included, Pro add-on

*API v2 (May)* — Better API for power users
Talk track: "10x rate limits, GraphQL, real-time webhooks"

*Do NOT promise:*
• Custom identity provider integrations
• Mobile app (needs dedicated team)
```

### View for Leadership

```
*Executive Roadmap*

*Strategic focus:* Enterprise readiness (SSO, API v2)

[P0] SSO — Enterprise — ON TRACK — 3 eng/6wk — $800K pipeline
[P0] API v2 — Platform — AT RISK — 4 eng/8wk — Top 10% retention
[P1] Onboarding — Growth — PLANNED Q3 — TBD — Trial conversion
[P2] Mobile — Expansion — PLANNED Q4+ — TBD — New segment

*Resource allocation:*
XX% enterprise | XX% platform | XX% growth

*Key risk:* API v2 schema migration
Mitigation: Phased rollout

*Decision needed:*
1. [Decision] — by [date]
```

### Dependencies View

```
*Dependency Map*

Identity Migration (DONE)
  └── SSO (IN PROGRESS)
      └── Enterprise Onboarding (PLANNED Q3)

Auth Refactor (IN PROGRESS)
  └── SSO — BLOCKED until refactor complete

*Critical path:*
SSO → Enterprise Onboarding → Enterprise Launch
Any SSO delay cascades to enterprise launch
```

## Design Principles

- **One roadmap, multiple views.** Data is the same. Framing changes per audience.
- **Now/Next/Later > dates.** Manage expectations, not commitments.
- **Customer impact is required.** Every initiative answers "what does this mean for users?"
- **Dependencies are the hidden risk.** The critical path determines real timeline.
- **Sales needs guardrails.** Tell them what to say AND what not to promise.
- **Leadership wants strategy, not features.** Connect to business outcomes.
