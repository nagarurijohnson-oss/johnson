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
**Status:** waiting — AUTO_Daily_Data_Load: confirmed step exists, awaiting time zone + folder decisions

**Done this session**
- Verified John_Mike_Customers_Amateur_Chef_Query exists and is viable as daily step

**Open items**
- User decides: time zone for 9:00 AM (IST or Central Standard Time)
- User decides: folder for AUTO_Daily_Data_Load (32393 or other)
- Create AUTO_Daily_Data_Load automation with chosen step, time zone, and folder
- Read back automation name, step, schedule, and status to confirm
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio UI
- Verify filtered table type, source, and row count (expect 10: TEST-CONTACT-006 to 015)
- Clarify: restore JMC-0004 FirstName from 'Updated' to 'Meera' or leave as-is
- Execute two-step method on JMC_Amateur_Chef_Filtered

**Decisions**
- Step for AUTO_Daily_Data_Load: John_Mike_Customers_Amateur_Chef_Query (SQL Query Activity, ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows
- API creation of filtered tables not viable; UI creation required
- Test PK constraint via insert-only route — CONFIRMED effective both runs
- Primary key ContactKey is enforced; insert-only rejects duplicates; upserts update instead

**Blockers**
- None

**Next**
- User replies with time zone (IST or CST) and folder (32393 or other)
- Create AUTO_Daily_Data_Load automation with John_Mike_Customers_Amateur_Chef_Query step and chosen schedule
- Read back automation name, step, schedule, and status to confirm

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
Yes, it exists. `John_Mike_Customers_Amateur_Chef_Query` is a SQL Query Activity in Automation Studio, not a file, and it's in the account now.

| | |
|---|---|
| Name | `John_Mike_Customers_Amateur_Chef_Query` |
| ID | `6aeb4e3d-2568-4f50-9acb-f469a7cce4c6` |
| External key | `John_Mike_Customers_Amateur_Chef_Que` (Marketing Cloud shortened it) |
| Query | `SELECT ContactKey, FirstName, Email, CreatedDate, Bio FROM [John_Mike_Customers] WHERE Bio = 'Amateur chef'` |
| Writes to | `John_Mike_Customers_Amateur_Chef` |
| Update type | **Overwrite** (the target table is cleared and refilled on each run) |
| Folder | 32395 |
| Created | 2026-10-06 10:07 (it hasn't been changed since) |

It can be the daily step for `AUTO_Daily_Data_Load`. I still need two more answers to build the automation:
- **Time zone for 9:00 AM:** India Standard Time or Central Standard Time
- **Automation folder:** 32393 or another one

You could reply "**a: John_Mike_Customers_Amateur_Chef_Query, IST, 32393**", for example. I'll take that as your go-ahead to create the automation, switch on its schedule and read it back to confirm.

Sources: checked live: Marketing Cloud (SQL Query activities filtered by name)

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
