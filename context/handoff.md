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
**Status:** blocked — Export steps added to automation; paused + wrong schedule + missing target table block execution

**Done this session**
- Added 3 export steps (DX, FT, Zip) to AUTO_Daily_Data_Load in correct order
- Confirmed all 4 steps read back with correct IDs and payload structure

**Open items**
- User resumes automation in UI after fixing schedule (currently paused)
- User opens AUTO_Daily_Data_Load Schedule UI, sets 9:00 AM India Standard Time, clicks Done and Save
- Recreate target table John_Mike_Customers_Amateur_Chef (5 fields: ContactKey PK, FirstName, Email, CreatedDate, Bio)
- Verify step 1 query points to recreated table after restoration
- Read back automation schedule to confirm 9:00 AM IST is stored
- Execute automation run to test dated file names (John_N_Orchestrate_Test_YYYYMMDD.zip)

**Decisions**
- Automation folder: 32393, time zone: India Standard Time, recurrence: daily
- Step 1: John_Mike_Customers_Amateur_Chef_Query (SQL Query Activity, ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
- Steps 2–4: DX export → FT move to Enhanced FTP Export → Zip with date stamp
- Payload shape: steps numbered from 0 with annotation labels

**Blockers**
- Automation paused (status PausedSchedule) — must be resumed after schedule fix
- Schedule stored as 2026-10-07T19:30 CST (8 Oct 7:00 AM IST) instead of 9:00 AM IST
- Target table John_Mike_Customers_Amateur_Chef missing — step 1 will fail on run

**Next**
- User recreates John_Mike_Customers_Amateur_Chef with 5 fields and ContactKey as primary key
- User opens AUTO_Daily_Data_Load in Automation Studio, fixes schedule to 9:00 AM IST, saves and resumes
- Verify step 1 query points to recreated table
- Read back schedule to confirm 9:00 AM IST stored correctly
- Execute automation to test dated export file names

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I've added the 3 export steps to `AUTO_Daily_Data_Load`, and the read-back confirms all 4 steps are in order. The automation is **paused**, though, so none of them will run until you resume it.

**Steps now in the automation**

| Step | Activity | Activity ID |
|---|---|---|
| 1 | `John_Mike_Customers_Amateur_Chef_Query` (SQL query, unchanged) | `6aeb4e3d-…` |
| 2 | `DX_John_N_Orchestrate_Test`: exports the table to a dated CSV | `91b446ef-…` |
| 3 | `FT_John_N_Orchestrate_Test_Export`: moves the CSV to the Enhanced FTP Export folder | `abaa02a4-…` |
| 4 | `DX_Zip_John_N_Orchestrate_Test`: zips it into `John_N_Orchestrate_Test_YYYYMMDD.zip` | `3e707142-…` |

**How I got there:** my first 3 attempts were rejected with `500 Internal Server Error` and no detail. A save with only step 1 worked, which showed the old query wasn't the cause. The fix was the payload shape: Marketing Cloud wanted steps numbered from 0 and labelled with `annotation`. The schedule wasn't changed.

**3 problems still open**
1. **It's paused.** The status is `PausedSchedule`. It was paused at 04:34 server time today, before this turn, and I didn't do it. If you resume it now, it runs at the wrong time (problem 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
