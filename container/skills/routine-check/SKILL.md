---
name: routine-check
description: Evening or weekly routine check. Calculate overdue and upcoming routines, suggest booking for significantly overdue items.
---

# Routine Check

Evening or weekly check on routine status. Read routine data, calculate what's overdue and coming up, and flag anything that needs booking.

## Data Source

Read `/workspace/group/routines.json` for last-done dates. Reference the routines skill for cadences and notes.

## Cadence Reference

| Routine | Every (days) |
|---------|-------------|
| Haircut | 14 |
| Massage | 21 |
| Facial | 28 |
| Chemical peel | 84 |
| EZ Gel (PRF) | 84 |
| Dermatologist | 91 |
| Dentist | 182 |
| DEXA scan | 182 |
| Physical | 365 |
| Fraxel Dual | 365 |
| KTP Laser | 365 |

## Logic

For each routine in `routines.json`:
1. Calculate days since `last_done`
2. Compare against cadence
3. Categorize:
   - **Overdue (2+ weeks past due):** Flag prominently, suggest booking
   - **Due now (within cadence window):** Note it's time
   - **Coming up (due within 7 days):** Mention as heads-up
   - **On track:** Skip unless doing a full report

## Output Format

**Quick check (evening):**
```
Routine check:
- Overdue: Massage (8 days past due). Book this week.
- Due now: Haircut (due tomorrow)
- Coming up: Facial in 5 days

Everything else on track.
```

**Full report (weekly / on request):**
Show all routines with days until due or days overdue.

## Escalation

- **2+ weeks overdue:** "This is significantly overdue. Want me to help you book it?"
- **Same routine overdue 3+ checks in a row:** "This keeps coming up. Let's just get it scheduled."
- **Treatment prep needed:** If a chemical peel is within 7 days, remind about tretinoin pause and LED mask pause (3 days before)

## Booking Help

If the user wants help booking, check `/workspace/group/providers.md` for provider contact info and booking details if the file exists. If not, ask for the provider info and offer to save it.

## Tone

Brief, practical. Don't nag — present the facts and offer to help. If everything is on track, say so in one line.
