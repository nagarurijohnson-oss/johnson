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
**Status:** on track — Found Meera row (JMC-0004); awaiting confirmation to update FirstName to 'Updated'

**Done this session**
- Located JMC-0004 (Meera) in John_Mike_Customers with Email meera.sample@example.com
- Verified row contents and table still has 5 rows

**Open items**
- Confirm update of JMC-0004 FirstName from 'Meera' to 'Updated'
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
- User confirms update of JMC-0004 FirstName to 'Updated'
- Execute upsert and verify FirstName changed; table remains 5 rows
- User selects template (A or B) for MCP_Email_Send_Test
- User updates TEST-CONTACT-001 phone in Contact Builder to 12758750001

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
I found the row. Nothing has been changed yet.

**One correction:** `John_Mike_Customers` has no field called `EmailAddress`. The field is named **`Email`**, so I matched on that. Exactly one row has `meera.sample@example.com`:

| ContactKey (primary key) | FirstName | Email | Bio | CreatedDate |
|---|---|---|---|---|
| JMC-0004 | Meera | meera.sample@example.com | Avid reader | 10/6/2026 9:48 AM |

**The change I'll make once you confirm**
- **Update the row:** upsert JMC-0004 in `John_Mike_Customers`, changing **FirstName from "Meera" to "Updated"**. Email, Bio and CreatedDate stay as they are, and no other rows change. The upsert matches on the primary key (ContactKey), not on Email, so it updates this one row and can't add a new one.
- **Check the result:** I'll read JMC-0004 back and confirm FirstName is "Updated" and the table still has 5 rows.

**This can be undone.** The old value is "Meera", recorded above, so I can put it back if you need me to.

**About the safety check:** I'll send the update without the confirmation flag first. If the check blocks it, I'll pass the flag based on your typed confirmation, the same way I did for the last insert, and I'll tell you if I do.

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
