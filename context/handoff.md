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
**Status:** blocked — Awaiting user answers to 3 questions: cut-off time, output table name, step position

**Done this session**
- Validated SQL syntax in Marketing Cloud
- Analyzed CreatedDate values in John_N_Orchestrate_Test (10 rows at 9:38:48 AM, 5 rows at 3:30:11 PM)
- Confirmed no suitable output table exists; JNOT_CreatedDate_0938_Filtered not found
- Verified John_N_Orchestrate_Test name is available for query

**Open items**
- User decides: cut-off timestamp (9:38:00 for all 15 rows, or 9:38:48 for 5 rows only)
- User decides: output table name (JNOT_CreatedAfter_0938 or alternative)
- User decides: step position (new step 1 before export, or step 5 at end)
- Create output table with 5 fields and ContactKey as primary key
- Create JNOT_CreatedAfter_0938_Query with user-chosen cut-off
- Add query as step to AUTO_Daily_Data_Load and verify step order
- Fix AUTO_Daily_Data_Load schedule from 7:00 AM IST to 9:00 AM IST and resume

**Decisions**
- Automation folder: 32393, time zone: India Standard Time, recurrence: daily
- Step 1: John_Mike_Customers_Amateur_Chef_Query (SQL Query Activity, ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
- Steps 2–4: DX export → FT move to Enhanced FTP Export → Zip with date stamp
- Output table will use Overwrite mode (clears only the new table each run)
- Output table folder: 49911 (source table's folder)

**Blockers**
- Automation paused (status PausedSchedule) — must be resumed after schedule fix
- Schedule stored as 2026-10-07T19:30 CST (8 Oct 7:00 AM IST) instead of 9:00 AM IST
- User must provide all three answers before query and table creation can proceed

**Next**
- User replies with all three answers in one message (e.g., '9:38:00, OK, step 5')
- Upon confirmation, create output table and read back fields to verify CreatedDate is Date type
- Create query with user-chosen cut-off and add to AUTO_Daily_Data_Load at chosen position
- Read back automation to verify new query step and existing steps 2–4 in correct order

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I haven't created anything yet. The checks turned up two things you need to decide first.

**What I found (read-only)**
- **The SQL is valid.** Marketing Cloud's validator accepted it with no errors.
- **The cut-off time decides the result.** `John_N_Orchestrate_Test` has 15 rows with only two CreatedDate values:
  - 10 rows at **10/6/2026 9:38:48 AM** (TEST-CONTACT-006 to 015)
  - 5 rows at **10/6/2026 3:30:11 PM** (TEST-CONTACT-001 to 005)

  If "after 9:38 AM" means after 9:38:00, the query returns **all 15 rows**. If it means after the 9:38:48 timestamp, it returns **only the 5 rows** from 3:30 PM. These times are in Marketing Cloud's server time zone (CST), not IST.
- **The query needs its own output table.** A query can't write its results back into the table it reads from. No suitable table exists: `JNOT_CreatedDate_0938_Filtered` isn't in the account. So I'd create one with the same 5 fields, ContactKey as the primary key, in the source table's folder (49911).
- **The name is free.** No existing query uses `John_N_Orchestrate_Test` in its name.

**Plan (once you answer)**
1. Create the table `JNOT_CreatedAfter_0938` and read its fields back to check CreatedDate is a Date fi

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
