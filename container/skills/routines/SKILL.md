---
name: routines
description: Track recurring personal routines (haircut, massage, facial, treatments, medical). Remind when overdue, help schedule, track completion dates.
---

# Routine Tracker

Shintaro has recurring personal care and medical routines. Track when each was last done and remind him when they're due.

## Routines & Cadences

| Routine | Every | Notes |
|---------|-------|-------|
| Haircut | 2 weeks | |
| Massage | 3 weeks | Recovery + stress management |
| Facial | 4 weeks | Skip in peel months (Jan, Apr, Jul, Oct) |
| Chemical peel (TCA + Jessner) | 12 weeks | Quarterly: Jan, Apr, Jul, Oct. Stop tretinoin 5-7 days before, resume 7-10 days after. No LED mask 3 days before. |
| EZ Gel (PRF) under-eye | 12 weeks | Feb, May, Aug, Nov (offset from peels by ~6 weeks) |
| Dermatologist | 13 weeks | Quarterly check-in |
| Dentist | 26 weeks | |
| DEXA scan | 26 weeks | Custom Fit SF. August (bulk checkpoint) + November (cut validation) in 2026 |
| Physical | 52 weeks | Annual |
| Fraxel Dual | 52 weeks | November/December, Victoria BC. Stop tretinoin 1 week before, resume 2 weeks after. |
| KTP Laser 532nm | 52 weeks | Under-eye vascular maintenance, annual |

## One-Time in 2026

- Sculptra assessment with Dr. He (Q2) — jawline definition
- Professional lymphatic drainage facial (Q2)
- Face gym trial (Q2)

## How to Track

Store routine data in `routines.json` in the group's data directory. Format:

```json
{
  "routines": {
    "haircut": {"last_done": "2026-03-01"},
    "massage": {"last_done": "2026-02-20"},
    "facial": {"last_done": "2026-02-15"}
  }
}
```

## Commands

When Shintaro asks about routines (e.g., "what's due", "routines", "when was my last haircut"):
1. Read `routines.json`
2. Calculate what's overdue and what's coming up
3. Present overdue items first, sorted by most overdue
4. Suggest booking if something is significantly overdue

When Shintaro says he completed a routine (e.g., "just got a haircut", "had my massage today"):
1. Update `routines.json` with today's date
2. Confirm and note when the next one is due

## Proactive Behavior

If routines are more than 1 week overdue, mention it when relevant. Don't nag every message, but do surface it naturally. If the same routine is overdue 3+ conversations in a row, escalate: "This keeps coming up. Want me to just help you book it?"
