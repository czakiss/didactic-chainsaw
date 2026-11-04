**Problem 1 of 3 split out of ticket #4471** — covers **379 of the 412 merged reports**
(the desk's own `CauseTable` view: 379 + 33 = 412).

## What happens

The shared date parser reads every date month-first (`MM/DD`). Every desk tenant writes the
day first (en-GB, en-IE, nl-NL, fr-FR, de-DE, it-IT, es-ES, pt-PT, pl-PL, cs-CZ, da-DK), so
a tenant's date comes out with month and day swapped: 4 March becomes 3 April, 1 December
becomes 12 January.

This is the one cause the desk already knows about: #4471's own page names it ("the parser
reads dates month first") and a fix is queued.

## Evidence

Counted with the desk's own view, as it was exported (`CauseTable` in the kb: `uniqueById`,
then `groupByCause` with `causeOf()` — any day-first tenant, any channel):

- Reports: **379 unique** — 204 app, 150 email, 25 form
- All 11 tenants affected; per tenant: harbour.dental 52, kettle.books 47, nine.lanterns 44,
  morrow.tax 40, long.table 39, ridge.clinic 36, stone.and.sons 30, lantern.row 28,
  alder.physio 23, pale.harbour 21, copper.studio 19
- First seen 2026-04-01, last seen 2026-10-04

Of these 379, the desk reads **5 reports as a one-day move** (its `desk-notes.json`,
`oneDayMove`) and files them under `parser` by tenant — footnoted there in the kb's
`CauseTable`. Those 5 are a third problem, filed as its own ticket here.

Example reports (id · tenant · channel):

- R-41206 · long.table · app — "Second time this month: 4 March turned into 3 April."
- R-41240 · morrow.tax · form — "Second time this month: 7 February turned into 2 July."
- R-41244 · lantern.row · email — "Second time this month: 1 December turned into 12 January."

## Fix

Already queued (per the kb incident page for #4471). This ticket covers the reports the
queued fix resolves; the 33 hint-cause reports are problem 2, the 5 one-day reports
problem 3.