---
name: process-doc
description: Generate structured process documentation — SOPs, playbooks, runbooks, RACI matrices, flowcharts. Use when someone says "write an SOP", "document this process", "create a playbook", "RACI for", "runbook", "process map", "standard operating procedure", "who does what", or needs to formalize any operational process.
---

# Process Documentation Generator

Turn tribal knowledge into structured, repeatable process documentation. SOPs, playbooks, runbooks, RACI matrices, and process flowcharts.

## Input

Parse the message to extract:
- **Document type** (required): SOP, playbook, runbook, RACI, or flowchart
- **Process or topic** (required): What process to document
- **Context** (optional): Existing steps, roles, pain points
- **Audience** (optional): Who will use this document

If the user doesn't specify a document type, infer from context:
- Day-to-day repeatable procedure → SOP
- Response to specific situations → Playbook
- Technical operational procedure → Runbook
- Role/responsibility clarity → RACI
- Visual process understanding → Flowchart

Examples:
- "write an SOP for customer onboarding"
- "playbook for handling enterprise escalations"
- "RACI for product launch"
- "runbook for incident response"

## Process

### Step 1: Gather Context

Ask clarifying questions if the process is underspecified:
- What triggers this process?
- Who are the key roles involved?
- What are the main steps?
- What goes wrong most often?

If the user provides enough context, proceed with reasonable defaults.

### Step 2: Generate the Document

Use the template matching the requested type:

#### SOP Template

```
*SOP: [Process Name]*

*Version:* 1.0
*Effective date:* [today]
*Owner:* [role/person]

*Purpose*
[Why this SOP exists and what outcome it ensures]

*Scope*
• Applies to: [roles, teams, situations]
• Does NOT apply to: [exclusions]

*Roles & Responsibilities*
• [Role 1]: [what they do]
• [Role 2]: [what they do]

*Prerequisites*
• [What must be true before starting]

*Procedure*

Step 1: [Action]
Who: [role] | When: [trigger]
[Detailed instructions]

Step 2: [Action]
Who: [role] | When: [timing]
[Detailed instructions]

Decision point: If [condition], go to Step 3a. Otherwise, Step 3b.

*Escalation*
• If [situation]: Escalate to [role] via [channel]

*Success Metric*
[How you know this process is working]
```

#### Playbook Template

```
*Playbook: [Situation Name]*

*Situation*
[What scenario triggers this playbook]

*Triggers — use when:*
• [Trigger 1]
• [Trigger 2]

*Response Framework*

Phase 1: Assess (first [X minutes])
• [Assessment action]
• Determine severity: Critical / High / Medium / Low

Phase 2: Respond
If Critical: [actions]
If High: [actions]
If Medium/Low: [actions]

Phase 3: Resolve
• [Resolution steps]
• [Verification steps]

Phase 4: Review (within [X days])
• Post-incident review
• Update this playbook if needed

*Rollback Plan*
If response makes things worse:
1. [Rollback step]
2. Escalate to [role]
```

#### RACI Template

```
*RACI Matrix: [Process/Project]*

Legend:
R = Responsible (does the work)
A = Accountable (final decision — exactly one per activity)
C = Consulted (input before decision)
I = Informed (notified after)

Activity: [Activity 1]
• R: [Role]
• A: [Role]
• C: [Role], [Role]
• I: [Role]

[Continue for each activity]

Rules:
• Every activity has exactly ONE "A"
• Minimize C's — too many slows decisions
```

#### Runbook Template

```
*Runbook: [Task]*

*Duration:* [estimated time]

Prerequisites:
• [Access/permissions needed]

Steps:

1. [Step name]
[Exact commands or actions]
Expected: [what you should see]
If unexpected: [what to do]

2. [Step name]
[Commands/actions]

3. Verification
[How to verify success]

Troubleshooting:
• [Issue]: [Resolution]

Rollback:
1. [Undo step]
```

### Step 3: Deliver

Send the document via send_message. Offer to save to Google Doc if they want to share it.

## Design Principles

- **A new person should be able to follow it.** No tribal knowledge required.
- **Decision points are explicit.** Every branch has clear criteria.
- **One accountable person per activity.** RACI breaks when accountability is shared.
- **Escalation paths are mandatory.** Every process needs a "what if this goes sideways" section.
- **Living documents.** Include version, owner, and review cadence.
