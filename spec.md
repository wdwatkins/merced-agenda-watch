# Merced Agenda Watch — report spec

Last changed: 2026-09-25

This file controls the weekly Merced Agenda Watch report. Edit it (by hand, or ask
Claude) to change anything about the report. The recurring cloud routine reads this
file on every run and follows it. When you change something meaningful, bump the
"Last changed" date above — the report footer echoes it.

---

## Sources to check

| Body | Legistar DepartmentDetail |
|------|---------------------------|
| City Council / Public Finance & Economic Development Authority / Parking Authority | `https://cityofmerced.legistar.com/DepartmentDetail.aspx?ID=29241&GUID=F41A62FB-62B9-4079-8961-E101311C972A` |
| Planning Commission | `https://cityofmerced.legistar.com/DepartmentDetail.aspx?ID=29250&GUID=E9B3998B-10D9-4820-8446-7F30ECE21B26` |

Per-meeting detail page (HTML list of agenda items, one per meeting):
`https://cityofmerced.legistar.com/MeetingDetail.aspx?ID=<id>&GUID=<guid>` — links come from the DepartmentDetail rows.

Full agenda packet PDF (use only for extra detail on flagged items):
`https://cityofmerced.legistar.com/View.ashx?M=A&ID=<id>&GUID=<guid>` — can be large; fetch selectively.

Not currently watched as full bodies (uncomment to add): Bicycle & Pedestrian Advisory Commission,
Recreation & Parks Commission, Merced County Board of Supervisors / County Planning Commission.

## Council subcommittees

Also check these five standing City Council subcommittees for newly published agendas
every run, using the same "what counts as new" window and rules as the main bodies:

| Subcommittee | Legistar DepartmentDetail |
|------|---------------------------|
| Ethics and Governance Subcommittee | `https://cityofmerced.legistar.com/DepartmentDetail.aspx?ID=56979&GUID=346D3D4E-7859-4D45-82E4-2834BF189EC3` |
| Finance and Economic Development Subcommittee | `https://cityofmerced.legistar.com/DepartmentDetail.aspx?ID=56977&GUID=FFCF1020-0335-4B1C-ADBE-231E33A9EF5A` |
| Public Safety Subcommittee | `https://cityofmerced.legistar.com/DepartmentDetail.aspx?ID=56975&GUID=A53DB38B-27CB-4CBF-AE40-5A1CBD52B8D7` |
| Public Works, Roads, and Infrastructure Subcommittee | `https://cityofmerced.legistar.com/DepartmentDetail.aspx?ID=56976&GUID=7F9FB0D8-0E3C-42FE-961B-0E89E798B4B5` |
| South Merced Subcommittee | `https://cityofmerced.legistar.com/DepartmentDetail.aspx?ID=56978&GUID=18257673-6828-421B-969F-08071C8E0E0D` |

If a subcommittee has a newly published agenda in the window, give it a condensed
summary (same one-bullet-per-item style as the main bodies) under its own
`## <Subcommittee name> — <date> · <N> items · [packet](<MeetingDetail url>)` heading,
placed after the City Council and Planning Commission sections. Run subcommittee
items through the same interest-topic flagging rules as everything else — a flagged
subcommittee item goes in the main Flagged items section like any other. Track
subcommittee meetings in `state.json`'s `seenAgendas` the same way (body = the
subcommittee's full name). These bodies meet irregularly with no fixed cadence —
most weeks none of them will have anything new, and that's normal, not a gap.

## What counts as "new" this run

- A meeting whose agenda has become **published** (row shows an "Agenda" or "Agenda Packet" link) since the last run.
- Look back ~10 days and ahead ~21 days from the run date.
- Also report a **newly posted cancellation notice** for a meeting that was previously watched.
- Track what has already been reported in `state.json` so items are not repeated week to week.
- If there is nothing new, produce the short "nothing new" report (see Format).

---

## Interest topics — expand and flag these

If an agenda item matches any bucket below, pull it into the **Flagged items**
section with a fuller write-up. Otherwise it goes in the condensed list.

**Annexation / city boundary**
annex, annexation, LAFCO, sphere of influence, reorganization, detachment,
prezoning, out-of-agency service agreement, growth boundary

**Street design / bike & pedestrian infrastructure**
bike lane, bicycle, cycle track, pedestrian, sidewalk, crosswalk, complete streets,
road diet, traffic calming, Active Transportation Program / ATP, corridor study,
roundabout, Class I/II/III path, multi-use trail, ADA curb ramp, street reconstruction,
streetscape, road realignment, speed limit, Vision Zero, grant for a transportation project

**Big-picture city finance**
budget, capital improvement program / CIP, bond, certificates of participation / COP,
debt issuance, tax, "Measure" + letter, general fund, fund balance, reserve policy,
structural deficit, development impact fee, fee study, rate study, utility rate increase,
mid-year budget review, year-end / fourth-quarter results, audit, ACFR,
pension / CalPERS / OPEB, sales tax or TOT trends, major grant award (>$1M)

**Always expand regardless of the buckets above**
General Plan / Comprehensive Plan update and any of its elements or study sessions;
EIR / major CEQA document; specific plan; zoning ordinance overhaul; housing element;
any item with no pre-written staff recommendation that sets new policy direction.

---

## Format

Markdown. Neutral, factual, terse. Explain significance; do not editorialize beyond
that. Where the item listing is thin, say so ("site not named in listing — packet
check needed") rather than guessing.

### Normal run

1. **Header** — `# Merced Agenda Watch — <Weekday> <Mon> <D>, <YYYY>, <run time>` and a line
   with the count of newly published agendas.
2. **Your topics this cycle** — one line: for each of the three interest buckets
   (Annexations / Street & bike-ped / Big-picture finance), state `none` or `N item(s)`.
3. **⚑ Flagged items** — for each: a bold heading `Body <date>, item <#> · <action type>`,
   then 2–4 sentences on what it is and why it matters, ending with a `[bucket]` tag.
   For flagged items, open the agenda packet PDF if needed to add: site/applicant/address,
   dollar amount, funding source, what changed vs. a prior action. Cap ~120 words each.
4. **Condensed list, per body** — `## <Body> — <date> · <N> items · [packet](<MeetingDetail url>)`
   then one bullet per remaining item: `**<item #> <type>:** <short subject>`.
   Collapse all closed-session items into one bullet. Cap 10 bullets per body; if more,
   add a final bullet summarizing the remainder. Include a section per subcommittee
   with a newly published agenda, per "Council subcommittees" above.
5. **Footer** — next meeting date for each body and whether its agenda is posted yet;
   source line (`City of Merced Legistar`); and `Spec last changed: <date from this file>`.

### Nothing-new run

One short paragraph: no agendas posted since the last run; next meeting date for each
body; whether their agendas are expected to post before next Friday. Then the footer line.

---

## Delivery

- **Repo archive:** write the report to `reports/<run-date>.md` (e.g. `reports/2026-10-02.md`)
  and copy it to `latest.md` at the repo root. Update `README.md`'s report list and
  "Latest report" link. Commit and push all changed files in one commit per run.
- **Artifact:** publish the report as an Artifact titled "Merced Agenda Watch",
  favicon 📋. `state.json` holds the current `artifactUrl` — pass it as `url` so the
  same link updates in place. If publishing fails, note it in the run output and continue.
- **Notification:** the routine run itself is the record; end the run with a one-line
  summary (counts + flagged headlines).
- Email / Slack: not configured.
