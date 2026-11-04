title: booking-v3 form hint says MM/DD/YYYY but parses day-first (33 reports of #4471)
labels: bug, 4471-review

**Problem 2 of 3 split out of ticket #4471** — covers **33 of the 412 merged reports** (8.0%).

## What happens

The `booking-v3` booking form prints the hint **MM/DD/YYYY** under its date field, so the
tenant's people type what the hint tells them — month first. The form then parses what they
typed the tenant's own way (day first). The result is the same symptom as the parser bug —
a booking on 1 June lands on 6 January — but it is a **different bug in a different place**:
the parser fix queued for #4471 does not touch it.

Only 3 tenants run `booking-v3`, and only reports that came in through the form on those
tenants are affected.

## Evidence

From the kb export's own logic (`causeOf()`: channel `form` on a `booking-v3` tenant):

- Reports: **33** — all channel `form`
- Tenants: alder.physio (de-DE) 12, copper.studio (es-ES) 11, pale.harbour (pt-PT) 10
- First seen 2026-04-17, last seen 2026-09-22
- Intake's `meta.intakeTag` guessed `hint` for only 18 of these 33; the other 15 are tagged
  `parser`. The tag reflects the reporter's browser, not the cause.

Example reports (id · tenant · tag):

- R-41241 · alder.physio · hint — "We had two people show up on 8 June. They were booked for 6 August."
- R-41230 · copper.studio · parser — "My client came on 1 June instead of 6 January. We sorted it out."
- R-41251 · pale.harbour · parser — "Wednesday 7 January showed as Wednesday 1 July. I moved it myself."

## Fix

Make booking-v3's hint print the tenant's real date order (`DD/MM/YYYY` for every day-first
tenant on v3), or make the form parse what the hint says. Neither is covered by the queued
parser fix.
