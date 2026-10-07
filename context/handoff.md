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
**Status:** blocked — I've created the 3 activities that export `John_N_Orchestrate_Test` to a zipped CSV.

**Done this session**
- I've created the 3 activities that export `John_N_Orchestrate_Test` to a zipped CSV. They aren't in an automation yet, because your reply picked option **c** but didn't name the automation. **Created (each one read back by ID)** | Step | A…

**Open items**
- Fix automation run time: user to open Schedule UI, set 9:00 AM India Standard Time, click Done and Save
- Recreate target table John_Mike_Customers_Amateur_Chef (5 fields: ContactKey PK, FirstName, Email, CreatedDate, Bio)
- Verify query points to recreated table after restoration
- Read back automation schedule after time correction to confirm 9:00 AM IST is stored
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio UI
- Verify filtered table type, source, and row count (expect 10: TEST-CONTACT-006 to 015)
- Clarify: restore JMC-0004 FirstName from 'Updated' to 'Meera' or leave as-is
- Execute two-step method on JMC_Amateur_Chef_Filtered

**Decisions**
- Step for AUTO_Daily_Data_Load: John_Mike_Customers_Amateur_Chef_Query (SQL Query Activity, ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
- Automation folder: 32393, time zone: India Standard Time, recurrence: daily
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition: within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows

**Blockers**
- Target table John_Mike_Customers_Amateur_Chef missing — automation will fail on each run until recreated
- Schedule stored as 2026-10-07T19:30 CST (8 Oct 7:00 AM IST) instead of 9:00 AM IST — user must correct in UI

**Next**
- User opens AUTO_Daily_Data_Load in Automation Studio (folder 32393), clicks Schedule, sets 9:00 AM India Standard Time, saves
- User confirms: recreate target table John_Mike_Customers_Amateur_Chef with 5 fields and ContactKey as primary key
- Verify query John_Mike_Customers_Amateur_Chef_Query points to recreated table
- Read back automation schedule to confirm 9:00 AM IST is now stored correctly

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I've created the 3 activities that export `John_N_Orchestrate_Test` to a zipped CSV. They aren't in an automation yet, because your reply picked option **c** but didn't name the automation.

**Created (each one read back by ID)**

| Step | Activity | ID | Confirmed |
|---|---|---|---|
| 1 | `DX_John_N_Orchestrate_Test` (Data Extension Extract) | `91b446ef-2182-4490-b38a-6b6f91976c78` | Source key `John_N_Orchestrate_Test`. Writes `John_N_Orchestrate_Test_%%Year%%%%Month%%%%Day%%.csv` with a header row, comma delimiter, text qualifiers and UTF-8 |
| 2 | `FT_John_N_Orchestrate_Test_Export` (File Transfer) | `abaa02a4-16d4-4294-8adb-dcb1aa3f2545` | Moves that CSV from the Safehouse to the Enhanced FTP Export folder, using the same location as the working example |
| 3 | `DX_Zip_John_N_Orchestrate_Test` (Zip extract) | `3e707142-c31f-49b0-9095-4d22932ccff7` | Zips the CSV into `John_N_Orchestrate_Test_%%Year%%%%Month%%%%Day%%.zip` in Export and keeps the CSV |

**How the timestamp works.** Each file name ends with the run date, e.g. `John_N_Orchestrate_Test_20261008.zip`. I didn't use the extract's built-in "add timestamp" option. It adds a time to the name that steps 2 and 3 couldn't 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
