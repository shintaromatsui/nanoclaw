---
name: calendar
description: View upcoming calendar events, check availability, and prep for meetings. Use when someone says "what's on my calendar", "show my schedule", "check my calendar", "am I free at [time]", "what meetings do I have", "who am I meeting with", "what's tomorrow look like", "calendar this week", or needs to view or check calendar events. Not for creating events — use schedule for that.
---

# Calendar

View upcoming calendar events with attendees. Use for meeting prep, daily planning, or checking availability.

**This is the READ skill. Use `schedule` for creating, updating, or deleting events.**

## When to Use

- "what's on my calendar" / "show me today"
- "what do I have tomorrow"
- "show me next week"
- "am I free at 3pm?"
- "who am I meeting with tomorrow"
- "what's Monday look like"

## Voice & Tone

**Personalized opener:** Warm, contextually relevant greeting — reference the time of day, how busy/free the day looks, or a recent meeting. Examples:
- "Hey Shintaro! Looks like you just wrapped up with Francois."
- "Hey Shintaro — you've been back to back today!"
- "Hey Shintaro! Quiet morning so far."
- "Hey Shintaro — pretty free day ahead."

**Conversational, not robotic:** No formal headers like "## Today's Events". Show the calendar naturally in the flow of conversation.

**Proactive:** End with an offer to help — "Want me to pull a brief on any of them?" or "Want me to schedule anything?"

## Process

### Step 1: Parse What's Being Asked

Determine the date range from the message:
- (empty / "today") → today
- "tomorrow" → tomorrow
- "next week" / "this week" → 7 days
- "Monday" / "this Friday" → that specific day
- "am I free at 3pm" → check availability for a specific time

### Step 2: Fetch Events

Use `mcp__google_calendar__list_events` with appropriate parameters:

```
timeMin: start of requested period (ISO 8601, America/Los_Angeles)
timeMax: end of requested period (ISO 8601, America/Los_Angeles)
maxResults: 20
```

For today: `timeMin` = start of today, `timeMax` = end of today (midnight).
For tomorrow: shift by one day.
For a week: `timeMax` = 7 days out.

### Step 3: Format Output

**Standard calendar view:**
```
Hey Shintaro! Hope the run went well this morning.

You have a moderately packed day today:

Friday, March 13th:

9:00 - 9:30AM: 1:1 with Wade
11:00 - 12:00PM: Product Review (Wade, Justin, +2 others)
3:00 - 4:00PM: Investor call

Want me to pull a brief on any of them?
```

**Availability check ("am I free at 3pm?"):**
```
Hey Shintaro!

You're free at 3pm — nothing until 4:30.

Want me to schedule something there?
```

```
Hey Shintaro!

3pm is taken — you have Product Review from 3:00 - 4:00PM (Wade, Justin, +2 others).

Next open slot is 4:00 - 5:30PM. Want to use that instead?
```

**"Who am I meeting with" view:**
```
Hey Shintaro!

Tomorrow you have 3 meetings:

- Wade Chambers (9:00 - 9:30AM)
- Francois Lebrun (11:00 - 11:30AM)
- Investor call — multiple attendees (2:00 - 3:00PM)

Want me to pull a dossier on any of them?
```

**Multi-day / week view:**
```
Hey Shintaro — here's the week ahead:

Monday, March 16th:
9:00 - 10:00AM: Team standup

Tuesday, March 17th:
No meetings — open day!

Wednesday, March 18th:
10:00 - 11:00AM: Cameron call (Zip)
3:00 - 4:00PM: 1:1 with Wade

Thursday, March 19th:
...

Want me to schedule anything else?
```

## Formatting Rules

- Times in 12-hour format: "9:00 - 9:30AM", "2:00 - 3:00PM"
- Show attendees: first 3 by name, then "+N others" if more
- Exclude yourself from the attendee list
- For all-day events (hotel, birthday, etc.): mention casually or skip unless relevant
- Empty days: "No meetings — open day!" not "0 events"
- Don't list internal Google Calendar metadata (IDs, raw emails unless needed)

## Anti-Patterns

- ❌ "Here's your calendar!" — just show it
- ❌ Formal headers like "## Today's Events"
- ❌ Long unstructured list of every calendar field
- ❌ Robotic checkmarks and bullet points for each event
- ❌ Showing the calendar owner in the attendee list
