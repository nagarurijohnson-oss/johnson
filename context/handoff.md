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
**Status:** on track — Bio field added to John_Mike_Customers (Text 20). Awaiting template choice for MCP_Email_Send_Test and phone number confirmation.

**Done this session**
- Added Bio field (Text, length 20, optional) to John_Mike_Customers
- Read back all 5 fields from John_Mike_Customers to verify save

**Open items**
- User confirms template choice (A or B) for MCP_Email_Send_Test creation
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test from chosen template
- User manually edits TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- Load sample rows into John_Mike_Customers DE, or make it sendable if user plans to email contacts
- Escalate persistent confirmation dialog issue to Orchestrate admin — blocking for 10 sessions, requires platform fix

**Decisions**
- Bio field: Text type, length 20 chars, optional, added to John_Mike_Customers
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields, not sendable
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields (added Bio), not sendable unless user specifies
- MCP_Email_Send_Test: will be created in folder 49889 with external key MCP_Email_Send_Test — awaiting template selection

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks IRREVERSIBLE modal display, preventing phone number update write (tenth consecutive session)
- Template choice (A or B) required before MCP_Email_Send_Test creation can proceed

**Next**
- User replies with template choice: A (TriggeredSendDataExtension) or B (SendLog) for MCP_Email_Send_Test
- Create MCP_Email_Send_Test from chosen template in folder 49889 with external key MCP_Email_Send_Test
- User manually updates TEST-CONTACT-001 phone in Contact Builder or requests admin enable confirmation dialog

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `4a65901d-f270-45ec-96fa-260777323520` |
**In its own words (excerpt):**
I added `Bio` to `John_Mike_Customers` and read the fields back to check it. It saved as you asked: Text, length 20, not a primary key, and can be left empty.

**Fields now on `John_Mike_Customers` (read back from Marketing Cloud)**

| # | Field | Type | Length | Primary key | Required |
|---|---|---|---|---|---|
| 1 | ContactKey | Text | 50 | Yes | Yes |
| 2 | FirstName | Text | 50 | No | No |
| 3 | Email | EmailAddress | 254 | No | No |
| 4 | CreatedDate | Date | — | No | No |
| 5 | **Bio** | **Text** | **20** | **No** | **No** |

The data extension now has 5 fields. The other four didn't change. I didn't touch any SQL queries.

**Still open:**
- **MCP_Email_Send_Test:** I'm still waiting for you to pick a template. Reply **A** for TriggeredSendDataExtension or **B** for SendLog.
- **TEST-CONTACT-001 phone number:** this change on `John_N_Orchestrate_Test` is still blocked because the confirmation step it needs isn't available here. You can change it to 12758750001 by hand in Contact Builder, or an Orchestrate admin can turn that confirmation step on.

Sources: engagement context (`context/handoff.md`, for the open items) · checked live: Marketing Cloud (added the field, then rea

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
