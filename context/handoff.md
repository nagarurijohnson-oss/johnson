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
**Status:** waiting — Awaiting three decisions on AUTO_Daily_Data_Load before build: step choice, time zone, folder

**Done this session**
- Confirmed AUTO_Daily_Data_Load name is available
- Mapped existing automation folders and schedules
- Identified Loyalty_Daily_Recognition stuck in Building (no steps)

**Open items**
- User decides: step for AUTO_Daily_Data_Load (existing activity or shell only)
- User decides: time zone for 9:00 AM (IST or Central Standard Time)
- User decides: folder for AUTO_Daily_Data_Load (32393 or other)
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio UI
- Verify filtered table type, source, and row count (expect 10: TEST-CONTACT-006 to 015)
- Clarify: restore JMC-0004 FirstName from 'Updated' to 'Meera' or leave as-is
- Execute two-step method on JMC_Amateur_Chef_Filtered
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder

**Decisions**
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
- User replies with three choices: step (1a/1b), time zone (IST/CST), folder (32393/other)
- Create AUTO_Daily_Data_Load automation with chosen step and schedule
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio
- Verify filtered table and clarify JMC-0004 FirstName restoration

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I haven't created anything yet. The name `AUTO_Daily_Data_Load` is free. Before I build it I need you to settle three things, because the answers change what gets created.

**What I checked (read-only)**
- No automation called `AUTO_Daily_Data_Load` exists in this business unit (27 automations in total).
- Most automations here sit in folder **32393**, and the Re-Engagement ones are in 49860.
- Existing schedules use either **Central Standard Time** or **India Standard Time**. You're on IST, so 9:00 AM could mean either.
- `Loyalty_Daily_Recognition` was created with no steps and is stuck in **Building** status with no schedule. An automation needs at least one activity before its schedule can be switched on.

**Three choices (reply with all three together)**
1. **What should it run?** Without a step it can be created but not actually scheduled to run.
   - (a) An existing activity, e.g. the SQL query `John_Mike_Customers_Amateur_Chef_Query` (refreshes `John_Mike_Customers_Amateur_Chef`). Name any other query, import or file transfer you want instead.
   - (b) No step for now. I create the shell with the Monday schedule saved but not active, and you or I add the step later.
2. **Ti

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
