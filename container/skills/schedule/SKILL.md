---
name: schedule
description: Create, update, or delete calendar events. Use when someone says "schedule a meeting", "book time with", "set up a call", "create an event", "block time for", "cancel my meeting", "move my meeting", "reschedule", "add to my calendar", or needs to create, modify, or delete calendar events. Not for viewing — use calendar for that.
---

# Schedule

Create, update, or delete calendar events.

**This is the WRITE skill. Use `calendar` for reading/viewing events.**

> **⚠️ CONFIRMATION REQUIRED:** Never create or delete events without explicit user approval. Always show what will happen and ask for confirmation first.

## When to Use

- "schedule a meeting with Sarah tomorrow at 3pm"
- "block 2 hours for deep work Friday morning"
- "cancel my 2pm"
- "move my 3pm to 4pm"
- "set up a call with Cameron next week"
- "add [event] to my calendar"

## Voice & Tone

- For action requests: jump straight to it — "Sure thing."
- Always confirm before acting (one clean summary, then "Create?" or "Done, good?")
- Catch conflicts proactively — check the calendar first, surface anything in the way
- For cancellations: ask if they want a note to the other participant

## Process

### Step 1: Detect Action Type

- "cancel" / "delete" → delete flow
- "move" / "reschedule" / "update" → update flow
- "free" / "when am I free" → availability check
- Everything else → create flow

### Step 2: Parse the Request

**For create — infer as much as possible:**

| Input | Infer |
|-------|-------|
| "meeting with Sarah" | Title: "Meeting with Sarah", look up Sarah's email via Notion |
| "1:1 with Wade" | Duration: 30 min |
| "lunch with John" | Duration: 60 min |
| No duration specified | Default: 60 min |
| "tomorrow at 3pm" | Parse datetime in America/Los_Angeles |

**Contact lookup via Notion:**
Use `mcp__notion__search` to find the person by name → get their email for the attendee field.
If multiple matches, show them and ask which one.
If no match, proceed without attendee and note it.

### Step 3: Check for Conflicts

Before creating, use `mcp__google_calendar__list_events` to check the proposed time slot.

Surface any conflicts: even "Free Time" blocks — mention it and ask if they want to book over it.

### Step 4: Confirm Before Acting

**Create confirmation:**
```
Sure thing.

You're free at 3pm. I'll create:

Meeting with Sarah (sarah@company.com)
Tuesday, March 17 at 3:00 PM (1 hour)

Create?
```

**With conflict:**
```
Sure thing.

I see a conflict at 3pm:
3:00 - 5:00PM: Free Time

Guessing I can book over that — confirm?
```

**Delete confirmation:**
```
Happy to.

Deleting:
Product Review — Wednesday, March 18 at 3:00 PM

Want me to include a cancellation note to attendees?
```

**Update confirmation:**
```
Sure thing.

Moving 1:1 with Wade from 2:00 PM → 4:00 PM. No conflicts at 4pm.

Move it?
```

### Step 5: Execute

**Create event:**
Use `mcp__google_calendar__create_event` with:
```
summary: "Meeting title"
start: { dateTime: "2026-03-17T15:00:00", timeZone: "America/Los_Angeles" }
end: { dateTime: "2026-03-17T16:00:00", timeZone: "America/Los_Angeles" }
description: "..." (optional)
location: "..." (optional)
attendees: [{ email: "sarah@company.com" }] (if found)
```

**Update event:**
First use `mcp__google_calendar__list_events` to find the event ID by title, then use `mcp__google_calendar__update_event`.

**Delete event:**
First find the event ID via `mcp__google_calendar__list_events`, then use `mcp__google_calendar__delete_event`.

### Step 6: Confirm Completion

```
Done! Added to your calendar.

Meeting with Sarah
Tuesday, March 17 at 3:00 - 4:00 PM
```

Or for reschedule:
```
Done — moved to 4pm. No conflicts.
```

## Finding Events by Title

When user says "cancel my Product Review" or "move my 2pm":
1. Use `mcp__google_calendar__list_events` for the next 7 days
2. Filter by matching title (case-insensitive contains)
3. If one match → proceed
4. If multiple matches → show them and ask which one
5. If no match → "I couldn't find that event. Can you check the exact title?"

## Availability Check

When user asks "when am I free tomorrow" or "find me 90 minutes Friday morning":
1. Fetch all events for that day
2. Calculate gaps in 9am-6pm working hours
3. Show open slots in a clean list

```
Tomorrow looks pretty open:

Open slots on Saturday, March 14th:
- 9:00 - 11:30AM (2.5 hrs)
- 12:00 - 6:00PM (6 hrs — after your lunch)

Want me to block any of these?
```

## Safety Rules

- **Never create or delete autonomously.** Always show what will happen and ask first.
- **No bulk operations.** One event at a time.
- **Ambiguous time → ask.** "Monday" when today is Monday — clarify which one.
- **Timezone always America/Los_Angeles** for display and API calls.

## Requires: Calendar Write Tools Unlocked

This skill needs `mcp__google_calendar__create_event`, `update_event`, and `delete_event` to be in the allowed tools list.

**One-line fix in `container/agent-runner/src/index.ts` (line ~486):**

Change:
```typescript
allowedTools.push('mcp__google_calendar__list_events', 'mcp__google_calendar__get_event');
```

To:
```typescript
allowedTools.push(
  'mcp__google_calendar__list_events',
  'mcp__google_calendar__get_event',
  'mcp__google_calendar__create_event',
  'mcp__google_calendar__update_event',
  'mcp__google_calendar__delete_event',
);
```

Then rebuild: `npm run build` from the project root.
