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
**Status:** waiting — AUTO_Daily_Data_Load: awaiting three decisions (step, time zone, folder) before build

**Done this session**
- Confirmed AUTO_Daily_Data_Load name is still available
- Re-presented three required decisions with full context and examples

**Open items**
- User decides: step for AUTO_Daily_Data_Load (existing query like John_Mike_Customers_Amateur_Chef_Query, or shell only)
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
- User replies with all three choices: step (a/b), time zone (IST/CST), folder (32393/other)
- Create AUTO_Daily_Data_Load automation with chosen step and schedule
- Read back automation name, step, schedule, and status to confirm
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I haven't created `AUTO_Daily_Data_Load` yet. I just checked again and the name is still free, but I need three decisions from you before I build it.

**1. What should it run each day?** An automation can only be switched on once it has at least one step. `Loyalty_Daily_Recognition` is an example: it was created with no steps and has been stuck in **Building** ever since.
- **(a) An existing SQL query.** For example, `John_Mike_Customers_Amateur_Chef_Query` refreshes `John_Mike_Customers_Amateur_Chef`, and `DE_Test_Customers_Gold_Refresh` refreshes the Gold table. There are 16 queries in this account, so name any of them. You can also name an import or file transfer.
- **(b) No step for now.** I create the automation with the daily 9:00 AM schedule saved, and it stays inactive until a step is added.

**2. Which time zone is 9:00 AM in?**
- **India Standard Time.** This matches your session.
- **Central Standard Time.** Other automations in this account use this one.

**3. Which folder should it go in?**
- **32393**, where most of the automations here live.
- **Another folder.** Give me the name or ID.

Reply with all three together, for example "**a: John_Mike_Customers_Amateur_Che

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
