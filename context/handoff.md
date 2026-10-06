# Handoff — current state

> **Rewritten at the end of every session.** This file is *now*; [`gotchas.md`](gotchas.md) is *forever*.
> If this file and [`../CONTEXT.md`](../CONTEXT.md) disagree, this one is newer.

**Last updated:** 2026-10-05 · **By:** <session or person>

---

## Where things stand

> **Not yet filled in.** — Where is the work right now, in two or three sentences? Someone picking
> this up cold reads this first.

## In progress

| What | State | Where it lives | Blocked on |
|---|---|---|---|
| | | | |

## Next steps

<!-- Ordered. The top item should be the one to do next, not the most interesting one. -->

1.

## Waiting on someone else

| What | Who | Since | Chased? |
|---|---|---|---|
| | | | |

## Things the next session should know

<!-- Anything true right now that is not obvious from the code: a half-finished refactor, a
     deliberately disabled test, a workaround that needs removing, a deploy that is half-applied.
     If you leave something in a strange state, this is where you say so. -->

-

<!-- orchestrate:session-state:start -->
<!-- Written by Orchestrate at the end of each session. Edits inside this block are
     replaced next session; anything OUTSIDE it is yours and is never touched. -->
### Engagement state — 2026-10-06
**Status:** waiting — Filtered table creation blocked by API; awaiting user to create in Email Studio UI (3 clicks)

**Done this session**
- None

**Open items**
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio from John_N_Orchestrate_Test + JNOT_CreatedDate_0938_Filter, replies 'done'
- Verify filtered table type (FilteredDataExtension), source (John_N_Orchestrate_Test), and row count (expect 10: TEST-CONTACT-006 to 015)
- Confirm date condition matches the 10 rows; if empty, switch to within-the-minute filter
- Execute two-step method on JMC_Amateur_Chef_Filtered (Email Studio steps from previous session)
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Verify both filtered tables report correct row counts when complete

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows
- Path forward: delete standard JNOT_CreatedDate_0938_Filtered and create filtered version in Email Studio
- API creation of filtered tables not viable; UI creation required

**Blockers**
- Marketing Cloud API has no endpoint for creating filtered tables; standard table endpoint lacks filter/source options; two candidate addresses return 404; filter-activity route returns 500

**Next**
- User creates filtered table in Email Studio: Subscribers → Data Extensions → John_N_Orchestrate_Test → Filter → JNOT_CreatedDate_0938_Filter → Save As JNOT_CreatedDate_0938_Filtered
- User replies 'done' when saved
- Verify filtered table type, source, and row count (expect 10 rows: TEST-CONTACT-006 to 015)

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I couldn't create the filtered table `JNOT_CreatedDate_0938_Filtered`. Nothing has been created or changed this turn.

**What I checked**
- **The name is free:** `JNOT_CreatedDate_0938_Filtered` doesn't exist, so the delete from last time held.
- **The saved filter is ready:** `JNOT_CreatedDate_0938_Filter` is on `John_N_Orchestrate_Test` with CreatedDate equal to 10/6/2026 9:38:48 AM. That's the 10 rows at 9:38 AM (TEST-CONTACT-006 to 015), as you chose earlier.
- **No new way to create one:**
  - The standard table-creation endpoint has no option for a filter or a source table.
  - Two other likely addresses for filtered tables both returned `404 Not Found`.
  - The filter-activity route the working example was built on has now returned `500 Internal Server Error` four times, with four different request formats.

Without a new approach, trying again would just repeat those errors.

**To finish it in Email Studio (about 3 clicks, filter already built):**
1. Go to **Email Studio → Subscribers → Data Extensions** and open `John_N_Orchestrate_Test` (folder 49911).
2. Click **Filter** and load the saved filter **`JNOT_CreatedDate_0938_Filter`**.
3. Click **Save As** and name it `JNOT_

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
