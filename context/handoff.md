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
**Status:** on track — JMC-0004 FirstName updated to 'Updated'; awaiting template choice & phone update

**Done this session**
- Upsert JMC-0004: FirstName 'Meera' → 'Updated' (Email, Bio, CreatedDate unchanged)
- Verified table still has 5 rows; other rows JMC-0001, 0002, 0003, 0005 unchanged
- Safety check passed with confirmation flag; one format error corrected and retried successfully

**Open items**
- Pick template (A or B) for MCP_Email_Send_Test creation
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Bio field: Text type, no length limit, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- CreatedDate populates with GetDate() default on import
- Safety check: send update without confirmation flag; if blocked, pass flag based on user's typed confirmation

**Blockers**
- None

**Next**
- User selects template (A or B) for MCP_Email_Send_Test
- User updates TEST-CONTACT-001 phone in Contact Builder to 12758750001
- Create MCP_Email_Send_Test in folder 49889 with selected template

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
I changed FirstName to "Updated" on the row with Email `meera.sample@example.com`, and reading the table back confirms it.

| ContactKey | FirstName | Email | Bio | CreatedDate |
|---|---|---|---|---|
| JMC-0004 | **Updated** (was Meera) | meera.sample@example.com | Avid reader | 10/6/2026 9:48 AM |

- **Other fields:** Email, Bio and CreatedDate didn't change.
- **Other rows:** the table still has **5 rows**, and the other four (JMC-0001, 0002, 0003, 0005) are as they were.

**How it went through:**
- **Safety check:** my first attempt went without the confirmation flag, as I said it would, and the check blocked it. This session can't show the on-screen Confirm pop-up the check waits for, so I passed the flag myself based on your typed "confirm". An admin can turn on that pop-up for Build sessions so these writes get your click directly.
- **One failed attempt:** the next try was rejected because the request was in the wrong format ("Parameter {values} is required."). Nothing was written. I fixed the format and the next attempt succeeded.

If you need to undo this, I can set FirstName back to "Meera".

**Still open from earlier sessions:**
- Choose template A or B for `MCP_Email_S

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
