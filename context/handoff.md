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
**Status:** waiting — Bio field (Text 20) ready to add to John_Mike_Customers — awaiting confirmation before write

**Done this session**
- Verified John_Mike_Customers has 4 fields, Bio name is available
- Proposed Bio field: Text type, length 20, optional

**Open items**
- User confirms Bio field length (20 chars vs 200/500) before adding to John_Mike_Customers
- Add Bio field to John_Mike_Customers and read back to verify
- User manually edits TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- Load sample rows into John_Mike_Customers DE, or make it sendable if user plans to email contacts
- Choose template (A or B) for MCP_Email_Send_Test data extension creation
- Escalate persistent confirmation dialog issue to Orchestrate admin — blocking for 9 sessions, requires platform fix

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID PK, Name, Email, Date), not sendable
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 4 fields (ContactKey PK, FirstName, Email, CreatedDate), not sendable unless user specifies
- MCP_Email_Send_Test: will be created in folder 49889 (MCP_Test) with external key MCP_Email_Send_Test — awaiting template selection
- Bio field: Text type proposed; length 20 chars (short, safer) vs 200/500 (more room for sentences) — user to decide

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks IRREVERSIBLE modal display, preventing phone number update write (ninth consecutive session)
- Template choice (A or B) required before MCP_Email_Send_Test creation can proceed
- Bio field length decision required before write to John_Mike_Customers

**Next**
- User confirms Bio field length: proceed with Text 20, or specify 200/500
- Add Bio field to John_Mike_Customers, read back to confirm save
- User replies with template choice: A (TriggeredSendDataExtension) or B (SendLog) for MCP_Email_Send_Test
- Create MCP_Email_Send_Test from chosen template in folder 49889 with external key MCP_Email_Send_Test

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `4a65901d-f270-45ec-96fa-260777323520` |
**In its own words (excerpt):**
I haven't changed anything yet. `John_Mike_Customers` has 4 fields and none of them is called `Bio`, so the name is free.

**Field to add**

| # | Field | Type | Length | Primary key | Required |
|---|---|---|---|---|---|
| 5 | Bio | Text | 20 | No | No (can be empty) |

**On the type:** Marketing Cloud field types are Text, Number, Date, Boolean, EmailAddress, Phone, Decimal and Locale. You asked for Text, and I'd use Text too. One thing to check is the length. 20 characters is very short for a bio, about three or four words. You can make a Text field longer later, but you can't make it shorter, so starting small is the safer choice. Still, if you want room for a sentence or two, 200 or 500 would suit better.

**Before you confirm:**
- **This can't be fully undone.** Once the field is added, you can't remove it through the API. Taking it out later would mean deleting it by hand in Contact Builder, or rebuilding the data extension.
- **SQL queries:** I created this data extension earlier today and don't expect any SQL Query activities to write to it. My check for queries that target it didn't run, because Marketing Cloud doesn't allow that filter. If you know of a query that writes

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
