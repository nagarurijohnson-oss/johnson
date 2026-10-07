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
**Status:** waiting — Query & table created, added to automation step 5. Awaiting: schedule fix to 9:00 AM IST + resume automation.

**Done this session**
- Created output table JNOT_CreatedAfter_0938 (ID 50f038ed-52c2-f111-a5e6-5cba2c19e778) with 5 fields, ContactKey PK, CreatedDate as Date type
- Created SQL query JNOT_CreatedAfter_0938_Query (ID 47de54c0-97de-4285-abf0-cd401ae5cd90) filtering CreatedDate > 2026-10-06 09:38:00
- Added query as step 5 to AUTO_Daily_Data_Load; verified all 5 steps in correct order
- Confirmed table in folder 49911, query in folder 32395, both read back successfully

**Open items**
- User fixes schedule in Automation Studio: set AUTO_Daily_Data_Load to 9:00 AM India Standard Time
- User resumes automation (change status from PausedSchedule to active)
- Confirm schedule fix by reading back automation after user saves
- Optional: run JNOT_CreatedAfter_0938_Query once before resuming to verify 15 rows load

**Decisions**
- Cut-off timestamp: 2026-10-06 09:38:00 (returns all 15 rows)
- Output table name: JNOT_CreatedAfter_0938
- Step position: step 5 (at end, after existing steps 1–4)
- Automation folder: 32393, time zone: India Standard Time, recurrence: daily
- Output table folder: 49911, Overwrite mode

**Blockers**
- Automation paused (status PausedSchedule) — must be resumed after schedule fix
- Schedule stored as 7:00 AM IST instead of 9:00 AM IST — must be corrected in Automation Studio

**Next**
- User opens AUTO_Daily_Data_Load in Automation Studio (folder 32393) → Schedule tab
- Set time to 9:00 AM, time zone to India Standard Time, save and make active
- Confirm schedule change by replying; I will read back automation to verify
- Automation will run at 9:00 AM IST daily; first run will load 15 rows into JNOT_CreatedAfter_0938

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I've added the query to `AUTO_Daily_Data_Load` as step 5 and checked everything by reading it back. Nothing has run yet: the automation is still paused.

**What I created**

| Item | Name | ID | Read back |
|---|---|---|---|
| Output table | `JNOT_CreatedAfter_0938` | `50f038ed-52c2-f111-a5e6-5cba2c19e778` | In folder 49911, 0 rows. It has the same 5 fields as the source table, and every field is required. **CreatedDate is a Date field**, and ContactKey is the primary key. |
| SQL query | `JNOT_CreatedAfter_0938_Query` | `47de54c0-97de-4285-abf0-cd401ae5cd90` | Runs `SELECT Email, CreatedDate, ContactKey, phone, Name FROM [John_N_Orchestrate_Test] WHERE CreatedDate > '2026-10-06 09:38:00'`. It **overwrites** `JNOT_CreatedAfter_0938` each run and is in folder 32395. |

**`AUTO_Daily_Data_Load` steps now**
1. `John_Mike_Customers_Amateur_Chef_Query`
2. `DX_John_N_Orchestrate_Test` (export to CSV)
3. `FT_John_N_Orchestrate_Test_Export` (move the CSV to the FTP Export folder)
4. `DX_Zip_John_N_Orchestrate_Test` (zip the CSV)
5. **`JNOT_CreatedAfter_0938_Query`** (new)

Steps 1–4 are the same as before, and the schedule wasn't changed.

**What the first run should do:** put all 15 rows 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
