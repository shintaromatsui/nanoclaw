---
name: booking
description: Book a haircut at Church Barber with Meelo via Squire. Use when someone says "book a haircut", "schedule a haircut", "book church barber", "I need a haircut", or when routine-check suggests booking a haircut.
allowed-tools: Bash(agent-browser:*), mcp__google_calendar__list_events
---

# Booking — Church Barber (Squire)

Book a Clipper Cut ($80) with Meelo Cervantes at Church Barber & Apothecary, SF, via Squire's web booking flow using `agent-browser`.

## Details

- **Shop:** Church Barber & Apothecary, San Francisco
- **Barber:** Meelo Cervantes ("Meelo C." on Squire)
- **Service:** Clipper Cut, $80
- **Booking URL:** `https://getsquire.com/booking/book/church-barber-and-apothecary-san-francisco/barber/meelo-cervantes/services?preselect=e162219c-611d-4f3d-9407-a8d0a00791c2`
- **Preferred day:** Saturday
- **Preferred time:** 10:00 - 11:00 AM
- **Payment:** Always select "pay in-store" — never enter payment info online

## Flow

### 1. Check if haircut is due

Read `/workspace/group/routines.json`. Check the haircut `last_done` date. If it's been fewer than 10 days, mention it's not quite due yet and ask if Shintaro still wants to book.

### 2. Check calendar for conflicts

Use `mcp__google_calendar__list_events` to check the preferred date (next Saturday by default, or whatever Shintaro requests). If there's a conflict in the morning window, suggest the next free Saturday morning or ask for a different preference.

### 3. Open the booking page

```bash
agent-browser open "https://getsquire.com/booking/book/church-barber-and-apothecary-san-francisco/barber/meelo-cervantes/services?preselect=e162219c-611d-4f3d-9407-a8d0a00791c2"
```

This URL pre-selects Meelo and the Clipper Cut service.

### 4. Handle the landing page

```bash
agent-browser snapshot -i
```

- If a cookie banner or popup appears, dismiss it (click accept/close)
- Re-snapshot after dismissing

### 5. Confirm service selection

The snapshot should show Clipper Cut pre-selected. Verify it shows:
- Barber: Meelo C.
- Service: Clipper Cut ($80)

Click the continue/next button to proceed to date selection.

### 6. Select date

```bash
agent-browser snapshot -i
```

On the date picker:
- Navigate to the preferred Saturday (or the date Shintaro requested)
- Click on that date
- If the date is grayed out / unavailable, snapshot the calendar and report the next 3 available dates to Shintaro

### 7. Select time slot

```bash
agent-browser snapshot -i
```

- Prefer a morning slot between 10:00 - 11:00 AM
- If no morning slots, pick the earliest available
- Click the preferred time slot

### 8. STOP — Get confirmation

**Do not proceed past this point without Shintaro's explicit confirmation.**

Send a message with the booking summary:

```
Ready to book:

Barber: Meelo Cervantes
Service: Clipper Cut
Price: $80
Date: [selected date]
Time: [selected time]
Payment: Pay in-store

Should I confirm this booking?
```

Wait for Shintaro to confirm before continuing.

### 9. Complete booking (after confirmation)

- On the checkout/confirmation page, select **"pay in-store"** as the payment method
- Fill in contact info if prompted (name: Shintaro Matsui)
- Click the final confirm/book button
- Wait for the confirmation page to load

```bash
agent-browser snapshot -i
```

Verify the booking confirmation is displayed. Screenshot it for reference:

```bash
agent-browser screenshot /tmp/booking-confirmation.png
```

### 10. Update routines

Update `/workspace/group/routines.json` — set the haircut `last_done` to the booked date.

### 11. Close browser

```bash
agent-browser close
```

Confirm the booking to Shintaro with the details.

## Error Handling

- **Page doesn't load / Squire is down:** Tell Shintaro and provide the direct booking URL so he can do it manually.
- **Barber not available on preferred date:** Show the next 3 available dates and ask which one works.
- **UI looks unfamiliar or unexpected:** Take a screenshot (`agent-browser screenshot /tmp/squire-debug.png`), describe what's visible, and ask Shintaro for guidance. Don't guess through unknown flows.
- **Any step fails:** Always run `agent-browser close` before stopping, whether the booking succeeded or failed.
- **Timeout or hang:** If a page takes more than 10 seconds, try `agent-browser reload` once. If still stuck, close and report.

## Anti-Patterns

- Never enter credit card or payment information — always "pay in-store"
- Never complete the booking without Shintaro's explicit confirmation
- Never skip the snapshot step — always re-snapshot after navigation
- Don't try to create a calendar event — the booking itself is the record
