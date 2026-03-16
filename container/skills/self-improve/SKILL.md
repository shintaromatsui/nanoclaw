# Self-Improvement

Capture learnings, errors, and corrections so you get better over time. This is always active — not triggered by a command.

## When to Log

| Signal | Category | File |
|--------|----------|------|
| User corrects you ("no", "that's wrong", "actually...") | `[correction]` | `intelligence.md` |
| You discover a preference (formatting, tone, timing) | `[preference]` | `intelligence.md` |
| A tool or API fails (MCP error, timeout, 404) | `[error]` | `errors.md` |
| A better approach is found for a recurring task | `[best-practice]` | `intelligence.md` |
| User asks for something you can't do | `[feature-request]` | `errors.md` |
| Your knowledge was wrong or outdated | `[knowledge-gap]` | `intelligence.md` |

## How to Log

Append to `/workspace/group/intelligence.md` or `/workspace/group/errors.md` using this format:

```
### [category] Short title
[YYYY-MM-DD] Context about what happened and what to do differently.
```

Examples:

```
### [correction] Don't use markdown headers in Telegram
[2026-03-14] Used ## headings in a message. Shintaro corrected — Telegram only supports *bold*, _italic_, • bullets, ```code```. No ## or **double stars**.

### [error] Calendar MCP fails when credentials expired
[2026-03-14] google_calendar MCP returned auth error. Credentials at ~/.calendar-mcp/credentials.json had expired. Solution: re-run OAuth flow.

### [feature-request] Send emails directly
[2026-03-14] Shintaro asked to send an email, but I can only draft. Need Gmail send capability.
```

## Pre-Task Review

Before starting these task types, scan `intelligence.md` and `errors.md` for relevant past entries:

- Research tasks — check for past corrections on format, length, depth
- Email drafts — check for voice/tone corrections
- Calendar/scheduling — check for past MCP errors
- Multi-step tasks — check for workflow corrections
- Any task similar to one that previously failed

Spend 5 seconds scanning, not 30. Just look for relevant entries — don't summarize them back to the user.

## Promotion

When you notice a pattern repeating (3+ related entries in `intelligence.md`), promote it:

1. Distill the pattern into a concise rule
2. Add it to the appropriate place:
   - Communication style → `/workspace/group/CLAUDE.md` formatting section
   - Task behavior → `/workspace/group/CLAUDE.md` rules section
   - Skill-specific → the relevant skill's `SKILL.md` file
3. Mark the original entries as promoted: append `(promoted to CLAUDE.md)` to the entry

## Weekly Synthesis

When running the weekly patterns synthesis (Sunday cron or manual):

1. Read all entries from the past week in `intelligence.md` and `errors.md`
2. Identify recurring themes
3. Promote any patterns that have solidified
4. Append a synthesis to `/workspace/group/patterns.md`:

```
## Week of YYYY-MM-DD
- [theme]: what was learned
- [promoted]: rule X added to CLAUDE.md
- [unresolved]: issues still occurring
```

## Files

| File | Purpose | Location |
|------|---------|----------|
| `intelligence.md` | Corrections, preferences, best practices, knowledge gaps | `/workspace/group/intelligence.md` |
| `errors.md` | Tool failures, API errors, feature requests, timeouts | `/workspace/group/errors.md` |
| `patterns.md` | Weekly synthesis of learnings | `/workspace/group/patterns.md` |
| `CLAUDE.md` | Promotion target for durable rules | `/workspace/group/CLAUDE.md` |

## Rules

- Log immediately when the trigger happens — don't wait until the end of the conversation
- Keep entries concise — 1-3 sentences max
- Include the fix or workaround, not just the problem
- Don't log trivial things (typos, one-off misunderstandings)
- Don't duplicate — check if a similar entry exists first, update it instead
- Never remove entries from `intelligence.md` — only mark as promoted or outdated
