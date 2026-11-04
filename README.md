# kb-4471-review

Review of support desk ticket **#4471** ("dates parse mm/dd in eu locales", marked *known*).
The desk merged 412 unique reports about wrong dates into one ticket. The reports do not
describe one problem: they describe three.

Filed here, one issue per problem, each with the number of reports it covers. Counts use
the desk's own view, as it was exported (`CauseTable`: `uniqueById`, then `groupByCause`
with `causeOf()`):

| # | Problem | Reports | Where they sit in the desk's view |
|---|---------|---------|-----------------------------------|
| 1 | [Shared parser reads every date month-first][i1] | 379 | the `parser` cause of #4471 (204 app / 150 email / 25 form; 5 of them footnoted by the desk as one-day moves — problem 3) |
| 2 | [booking-v3 hint says MM/DD/YYYY but the form parses day-first][i2] | 33 | the `hint` cause of #4471 (all form; 3 tenants on booking-v3) |
| 3 | [Invites shifted by one day (timezone/DST), not a month swap][i3] | 5 | counted under `parser` in #4471, footnoted by the desk (`desk-notes.json` → `oneDayMove`) |

The desk's exported view counts 379 + 33 = 412 unique reports; the 15 duplicate rows in
the export (overlapping export pages) are removed by the kb's own `uniqueById`. The 5
one-day reports sit inside the 379, so the tickets deliberately overlap by 5: the desk's
view files them under `parser`, its notes read them as a different problem.

## The kb page

The challenge asks for a page about these problems, added to the kb, in the kb's own format
(`.svx`, frontmatter with a `signature`, ending with `<RenderStamp {signature} />`):

- [`kb/src/routes/kb/incidents/4471-review/+page.svx`][svx] — the page source
- [`kb/incidents-4471-review.html`][html] — the page as the desk will see it (static render)

## Data

- `data/reports-4471.json` — the export from the ticket system (427 rows, 412 unique)
- `data/desk-notes.json` — the desk's own notes (`oneDayMove`)
- `data/tenants/` — the tenant directory: locale and booking form per tenant
- `kb/src/lib/kb/causes.ts` — the kb's own cause logic, unchanged (the reference for the split)

[i1]: issues/2
[i2]: issues/3
[i3]: issues/4
[svx]: blob/main/kb/src/routes/kb/incidents/4471-review/%2Bpage.svx
[html]: blob/main/kb/incidents-4471-review.html
