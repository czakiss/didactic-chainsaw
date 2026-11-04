# kb-4471-review

Review of support desk ticket **#4471** ("dates parse mm/dd in eu locales", marked *known*).
The desk merged 412 unique reports about wrong dates into one ticket. The reports do not
describe one problem: they describe three.

Filed here, one issue per problem, each with the number of reports it covers:

| # | Problem | Reports | Source |
|---|---------|---------|--------|
| 1 | [Shared parser reads every date month-first][i1] | 374 | `causeOf()` in the kb export: any day-first tenant, any channel |
| 2 | [booking-v3 hint says MM/DD/YYYY but the form parses day-first][i2] | 33 | `causeOf()`: channel `form` on a `booking-v3` tenant |
| 3 | [Invites shifted by one day (timezone/DST), not a month swap][i3] | 5 | `desk-notes.json` → `oneDayMove` |

374 + 33 + 5 = 412 unique reports. The export carries 427 rows; 15 are duplicated report ids
(the ticket system exports in overlapping pages), removed the same way the kb's own
`uniqueById` removes them.

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

[i1]: issues/1
[i2]: issues/2
[i3]: issues/3
[svx]: blob/main/kb/src/routes/kb/incidents/4471-review/%2Bpage.svx
[html]: blob/main/kb/incidents-4471-review.html
