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
### Engagement state — 2026-10-07
**Status:** waiting — Automation 5/6 steps built & paused. Awaiting cutoff decision (A: 15 rows | B: 5 rows) + step order confirmation before adding SQL Query st…

**Done this session**
- Verified John_N_Orchestrate_Test has 15 rows with two CreatedDate timestamps (10/6/2026 9:38:48 AM and 3:30:11 PM)
- Confirmed AUTO_Orchestrate_Full_Test remains paused with 5 steps intact, daily 9:00 AM IST schedule unchanged

**Open items**
- User decision: cutoff filter option A (15 rows) or B (5 rows) for SQL Query
- User decision: add SQL Query as step 6 at end or move before Script step 5 for logging
- Create TEST_SQL_Output table in folder 49911 with ContactKey, Name, Email, phone, CreatedDate
- Create ACT_SQL_Test query with chosen cutoff, targeting TEST_SQL_Output
- Add ACT_SQL_Test to AUTO_Orchestrate_Full_Test at confirmed step position
- Add Send Email activity as step (manual UI creation required)
- Run automation once to test all steps end-to-end
- Verify TEST_FullTest_Script_Log row counts and TEST_SQL_Output results

**Decisions**
- Data Copy implemented as SQL query (table-to-table), not Import activity
- Send Email step deferred to manual UI creation due to API limitation
- Script logs row counts for SQL output and Data Copy only
- Automation schedule: daily 9:00 AM IST, status Paused, first run 8 Oct

**Blockers**
- Send Email activity cannot be created via API—nested send classification settings rejected; manual UI step required
- Cutoff timestamp ambiguity: CreatedDate boundary at 2026-10-06 09:38:48 AM determines 15 vs 5 rows—awaiting user choice

**Next**
- User replies with cutoff choice (A or B) and step 6 position confirmation
- Create TEST_SQL_Output table and ACT_SQL_Test query with chosen parameters
- Add SQL Query step to automation at confirmed position
- Read back table, query, and automation to verify configuration
- User adds Send Email step 6 (or 7) manually in Automation Studio UI

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `f203b158-e2aa-4e90-b9af-ee68c9f98be8` |
**In its own words (excerpt):**
I haven't created anything yet. There's one decision for you first, because "after 9:38 AM" catches either every row in the table or only a third of them.

## What I found
- **`TEST_SQL_Output` doesn't exist**, so I'd create it. `ACT_SQL_Test` doesn't exist yet either.
- **`John_N_Orchestrate_Test` has 15 rows, with only two CreatedDate values:**
  - 10 rows (TEST-CONTACT-006 to 015) at **10/6/2026 9:38:48 AM**
  - 5 rows (TEST-CONTACT-001 to 005) at **10/6/2026 3:30:11 PM**
- **The automation** has 5 steps and is still Paused, with the daily 9:00 AM IST schedule unchanged.

## The cutoff question
Your cutoff lands in the same minute as those 10 rows, so the exact boundary decides the result:

| Option | Filter | Rows returned |
|---|---|---|
| **A** | `CreatedDate > '2026-10-06 09:38:00'` (from the start of the minute) | **15**, which is the whole table |
| **B** | `CreatedDate > '2026-10-06 09:38:48'` (strictly after those 10 rows) | **5**, only the 3:30 PM rows |

I'll compare against the timestamps exactly as they're stored in the table, with no time-zone conversion. That matches how the values above were loaded.

## What I'll do once you choose
1. **Create the table `TEST_SQL_

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
