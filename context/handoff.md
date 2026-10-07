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
**Status:** blocked — Awaiting 3 decisions on active customer definition, write mode, and step position before query creation

**Done this session**
- Confirmed John_Mike_Customers has no 'active' field
- Validated _Subscribers.Status='active' query syntax
- Identified target table requires all 5 fields (Email, CreatedDate, ContactKey, phone, Name)
- Noted target already has 15 rows; Overwrite would delete them

**Open items**
- User decides: active customer source (a: _Subscribers with placeholders, b: new IsActive field, c: other)
- User decides: write mode (Update to keep 15 rows, or Overwrite to replace)
- User decides: step position (new step 1 before export, or step 5 at end)
- User recreates John_Mike_Customers_Amateur_Chef with 5 fields and ContactKey as primary key
- User opens AUTO_Daily_Data_Load, fixes schedule to 9:00 AM IST, saves and resumes
- Verify step 1 query points to recreated table
- Read back schedule to confirm 9:00 AM IST stored correctly
- Execute automation to test dated export file names

**Decisions**
- Automation folder: 32393, time zone: India Standard Time, recurrence: daily
- Step 1: John_Mike_Customers_Amateur_Chef_Query (SQL Query Activity, ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
- Steps 2–4: DX export → FT move to Enhanced FTP Export → Zip with date stamp
- Payload shape: steps numbered from 0 with annotation labels
- Target table ___John_Mike_Customers_Amateur_Chef_1 exists with 1 row (renamed, not deleted)

**Blockers**
- Automation paused (status PausedSchedule) — must be resumed after schedule fix
- Schedule stored as 2026-10-07T19:30 CST (8 Oct 7:00 AM IST) instead of 9:00 AM IST
- Three decisions required before creating active customer query

**Next**
- User provides answers to all three questions (active source, write mode, step position) in one reply
- Upon confirmation, create John_N_Orchestrate_Test_Active_Customers_Query and add to AUTO_Daily_Data_Load
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
I haven't created anything yet. "Active customers" doesn't match any field in this account, and the target table's setup affects what the query can write, so I need you to make three decisions first.

**What I found (read-only)**
- **No customer table has an "active" field.** `John_Mike_Customers` has ContactKey, FirstName, Email, CreatedDate and Bio. Searches for "Customer" and "Active" found no other tables.
- **The system view `_Subscribers` does have one.** Its `Status` field is `'active'` for subscribers who can receive email. I validated this query and it's valid:
  `SELECT SubscriberKey AS ContactKey, EmailAddress AS Email, DateJoined AS CreatedDate FROM _Subscribers WHERE Status = 'active'`
- **The target needs every field filled in.** All 5 fields in `John_N_Orchestrate_Test` are required: Email, CreatedDate, ContactKey (primary key), phone and Name. `_Subscribers` has no phone or name, so rows without them would be rejected.
- **The target already has 15 rows.** An Overwrite would delete them on every run.
- **Position in the automation.** Steps 2–4 export `John_N_Orchestrate_Test`, so the new query should run before the export. Otherwise the file is a day old.
- Correcti

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
