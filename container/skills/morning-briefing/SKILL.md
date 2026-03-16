---
name: morning-briefing
description: Morning briefing for cron delivery. Check routines, todos, and goals. Send a scannable summary via send_message.
---

# Morning Briefing

Automated morning briefing delivered via cron. Gather status across routines, todos, and goals, then send a concise summary using `send_message`.

## Data Gathering

1. **Read `/workspace/group/routines.json`** — find what's due or overdue today
2. **Read `/workspace/group/todos.json`** — get open items, especially high-priority
3. **Reference the goals skill** — check daily commitments
4. **Run `date`** — get current day of week for weekly rhythm items

## Message Structure

Keep it scannable. No walls of text. Use this skeleton:

```
Good morning. Here's your briefing for [Day, Date]:

ROUTINES
- [Overdue]: Haircut (3 days overdue)
- [Due soon]: Massage (due in 2 days)
- [None overdue — skip this section]

TODAY'S FOCUS
- Daily: One career action, hit calories, workout
- [Day-specific from goals weekly rhythm, e.g., "Monday: review pipeline"]
- High-priority todo: [top item]

OPEN ITEMS
- [N] open todos ([N] high priority)
- Stale: [any items 2+ weeks old]

[Optional one-liner if something notable, e.g., "Chemical peel scheduled this week — stop tretinoin by Wednesday."]
```

## Day-Specific Items

From the goals skill weekly rhythm:
- **Monday:** Review career pipeline
- **Wednesday:** Follow-ups
- **Friday:** Deep research on 1 company
- **Sunday:** Weekly check-in + run

## Rules

- **Omit empty sections** — if no routines are overdue, skip that block
- **Keep it under 15 lines** — this is a glance, not a report
- **Flag treatment prep** — if a chemical peel or Fraxel is within 7 days, remind about tretinoin pause
- **Don't coach** — save that for when he asks. Just present facts
- **Send via `send_message`** — this is a cron-triggered skill, not interactive

## Delivery

Use the `send_message` bash tool to deliver the briefing to the group's channel. The message should be ready to read with no follow-up needed.
