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
**Status:** at risk — AUTO_Daily_Data_Load created but two critical issues: wrong run time (7 AM not 9 AM IST) and target table missing

**Done this session**
- Created AUTO_Daily_Data_Load automation in folder 32393, India Standard Time, daily recurrence
- Confirmed step John_Mike_Customers_Amateur_Chef_Query is attached
- Identified time zone conversion bug: activation shifted schedule from 9:00 AM to 7:00 AM IST

**Open items**
- Fix automation run time: set 9:00 AM IST in Automation Studio Schedule UI or pause and retry API
- Recreate target table John_Mike_Customers_Amateur_Chef (5 fields, ContactKey PK) — currently missing/deleted
- Verify query points to recreated table after table restoration
- Read back automation schedule after time correction to confirm 9:00 AM IST is stored
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio UI
- Verify filtered table type, source, and row count (expect 10: TEST-CONTACT-006 to 015)
- Clarify: restore JMC-0004 FirstName from 'Updated' to 'Meera' or leave as-is
- Execute two-step method on JMC_Amateur_Chef_Filtered

**Decisions**
- Step for AUTO_Daily_Data_Load: John_Mike_Customers_Amateur_Chef_Query (SQL Query Activity, ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
- Automation folder: 32393
- Time zone: India Standard Time
- Recurrence: daily
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows

**Blockers**
- Target table John_Mike_Customers_Amateur_Chef missing — automation will fail on each run
- Schedule activation tool shifted 9:00 AM IST to 7:00 AM IST; UI correction or API retry needed

**Next**
- User confirms: fix time in UI or pause automation for API retry
- User confirms: recreate target table John_Mike_Customers_Amateur_Chef now
- Recreate table with 5 fields (ContactKey, FirstName, Email, CreatedDate, Bio) and ContactKey as primary key
- Verify query John_Mike_Customers_Amateur_Chef_Query points to recreated table
- Read back automation schedule after time correction to confirm 9:00 AM IST stored correctly

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I created `AUTO_Daily_Data_Load` and switched it on, but I found two problems. As it stands it won't do what you asked: the run time is wrong, and the table its step writes to looks to be missing.

**What's in place (confirmed by reading it back)**
- **Automation:** `AUTO_Daily_Data_Load` (ID `21f21dab-f5f1-4ef9-950c-21ebd13e7cbb`), folder 32393, status **Scheduled**, recurrence daily, time zone India Standard Time.
- **Step 1:** `John_Mike_Customers_Amateur_Chef_Query`.
- Marketing Cloud dropped the schedule from the first create request, so I added it with an update and then switched it on.

**Problem 1: it will run at 7:00 AM IST, not 9:00.**
- Before I switched it on, the stored start was 7 Oct, 9:00 AM IST.
- Switching it on moved the start, and the read-back now shows **8 Oct at 7:00 AM IST**. Marketing Cloud stores times in its own server zone, CST (UTC−6), which is where this conversion comes from: 2026-10-07 19:30 CST is 8 Oct 7:00 AM IST.
- So it would skip 7 Oct and then run 2 hours early every day.
- The shift happened inside Orchestrate's schedule-activation tool, and I can't predict it well enough to set a "corrected" time reliably.

**Problem 2: the query's target ta

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
