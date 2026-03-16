---
name: status
description: Quick status overview across all goal areas. Read todos and routines, reference goals, keep it scannable.
---

# Status Overview

When Shintaro asks for "status", "how am I doing", "overview", or "dashboard", give a concise snapshot across all goal areas.

## Data Sources

1. **Read `/workspace/group/todos.json`** — count open items per goal area, note high-priority items
2. **Read `/workspace/group/routines.json`** — check what's overdue, what's coming up
3. **Reference the goals skill** — for targets and key results per area

## Output Format

One to two lines per goal area. Use status indicators:

```
Career: 2 open todos (1 high). Last outreach: 3 days ago. Pipeline needs attention.
Body: On track — logged 4 workouts this week. Calories consistent.
Face: Skincare streak intact. Chemical peel due in 2 weeks.
Financial: No open action items. Next check-in: end of month.
Awai: 1 todo (event planning). No movement in 2 weeks.
Self: Bedtime consistent. Sunday check-in done.
```

## Rules

- **Lead with what needs attention** — put problem areas first
- **Skip areas that are fine** if the user seems busy — just flag what matters
- **Note overdue routines** inline with the relevant goal (e.g., facial overdue goes under Face)
- **Flag stale todos** — anything open 2+ weeks gets called out
- **Don't editorialize** — facts and status, not a pep talk. Save coaching for when he asks

## Tone

Scannable, factual, brief. Think executive dashboard, not essay. If everything is on track, say so in one line: "All areas green. Biggest open item: [X]."
