---
name: todos
description: Quick-capture todo list and task management. Add, view, complete, and prioritize tasks. Suggest next actions based on goals and context.
---

# Todo System

Shintaro's quick-capture task list. Keep it simple — a flat list with status, not a complex project management system.

## Storage

Store todos in `todos.json` in the group's data directory:

```json
{
  "todos": [
    {
      "id": 1,
      "text": "Follow up with recruiter at Anthropic",
      "added": "2026-03-12",
      "completed": null,
      "goal": "career",
      "priority": "high"
    }
  ],
  "next_id": 2
}
```

## Commands

**Add a todo:**
When Shintaro says "add to my list", "todo", "remind me to", etc.:
- Capture the item
- Auto-tag with goal if obvious (career, body, face, financial, awai, self)
- Set priority (high/medium/low) based on context
- Confirm briefly

**View todos:**
When Shintaro says "todos", "what's on my list", "what do I need to do":
- Show open items grouped by priority
- Note any that are related to today's goal commitments
- If items are stale (2+ weeks old), flag them

**Complete a todo:**
When Shintaro says "done with X", "finished X", "completed X":
- Mark as completed with today's date
- Brief acknowledgment

**What's next:**
When Shintaro says "what should I do", "what's next", "whats-next":
- Look at open todos
- Cross-reference with his goal priorities and daily commitments
- Suggest the highest-leverage item
- If it's morning: emphasize the "one career action" from his journaling habit
- If nothing urgent: suggest a goal-advancing action

## Priority Logic

- **High:** Time-sensitive, blocks other work, career-related during job search
- **Medium:** Important but not urgent, goal-advancing
- **Low:** Nice to have, can wait

## Tone

Keep it brief. "Added." / "Done." / "3 open items, highest priority: follow up with Anthropic recruiter." Don't over-explain.
