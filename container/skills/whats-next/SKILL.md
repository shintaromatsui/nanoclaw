---
name: whats-next
description: Suggest Shintaro's highest-leverage next action based on open todos, goal priorities, time of day, and recent activity.
---

# What's Next

When Shintaro asks "what should I do", "what's next", or seems unsure where to focus, analyze context and suggest the single highest-leverage action.

## How to Decide

1. **Read `/workspace/group/todos.json`** for open items
2. **Check the time of day** (use `date` command)
3. **Cross-reference the goals skill** for current priorities and daily commitments
4. **Consider recency** — what has he already done today? Don't suggest what's already handled

## Time-of-Day Logic

**Morning (before 11am):**
- Emphasize the "one career action" from his daily commitment
- Career-related todos get priority boost
- If no career todos exist, suggest: "What's your one career action today?"

**Midday (11am-5pm):**
- Focus on high-priority open todos
- Body/workout tasks if not yet done
- Deep work items (research, follow-ups)

**Evening (after 5pm):**
- Wind-down tasks: skincare routine, LED mask, journaling
- Low-effort admin tasks
- Planning for tomorrow
- Don't suggest career outreach — it's not the time

## Priority Stack

1. **Overdue high-priority todos** — anything time-sensitive or blocking
2. **Daily commitments not yet done** — career action, calories, workout, skincare
3. **Medium-priority todos** aligned with current top goal
4. **Stale items** — anything sitting 2+ weeks, either do it or kill it
5. **Goal-advancing actions** — if the list is clear, suggest proactive moves

## Output Format

Keep it tight. One clear recommendation with brief reasoning:

> **Follow up with the Anthropic recruiter.** It's morning, and you haven't done your career action today. This one's been sitting 3 days.

If there are 2-3 close contenders, mention them briefly:

> After that: gym (you haven't logged a workout today) or knock out that dentist booking.

## Tone

Direct, not preachy. Don't list every open todo — he can ask for that separately. The point is to cut through decision paralysis and give him one thing to do right now.
