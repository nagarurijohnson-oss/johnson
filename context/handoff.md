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
**Status:** waiting — Waiting for template choice (A/B) before creating MCP_Email_Send_Test data extension

**Done this session**
- Verified MCP_Test folder (ID 49889) exists and can hold data extensions
- Confirmed MCP_Email_Send_Test name is available
- Identified 22 templates in account; no 'Email Send' template exists
- Presented two closest options: TriggeredSendDataExtension (A) vs SendLog (B)

**Open items**
- User manually edits TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- Load sample rows into John_Mike_Customers DE, or make it sendable if user plans to email contacts
- Escalate persistent confirmation dialog issue to Orchestrate admin — blocking for 9 sessions, requires platform fix
- Choose template (A or B) for MCP_Email_Send_Test data extension creation

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID PK, Name, Email, Date), not sendable
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 4 fields (ContactKey PK, FirstName, Email, CreatedDate), not sendable unless user specifies
- MCP_Email_Send_Test: will be created in folder 49889 (MCP_Test) with external key MCP_Email_Send_Test — awaiting template selection

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks IRREVERSIBLE modal display, preventing phone number update write (ninth consecutive session)
- Template choice required before MCP_Email_Send_Test creation can proceed

**Next**
- User replies with template choice: A (TriggeredSendDataExtension, recommended) or B (SendLog)
- Create MCP_Email_Send_Test from chosen template in folder 49889 with external key MCP_Email_Send_Test
- Read back folder, template, sendable setting and fields to confirm creation
- Unblock phone update: user manually edits in Contact Builder OR admin enables confirmation dialog

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `4a65901d-f270-45ec-96fa-260777323520` |
**In its own words (excerpt):**
I haven't created anything yet. This Marketing Cloud account has no data extension template named "Email Send", so I need you to choose which template to use.

**What I found:**
- **Folder:** `MCP_Test` (ID 49889) is a Data Extensions folder, so it can hold the new data extension.
- **Name:** no existing data extension is called `MCP_Email_Send_Test`, so the name is free.
- **Templates:** the account has 22 data extension templates, and none is called "Email Send". These two are the closest to an email send:

| Option | Template | What it's for |
|---|---|---|
| **A** | **TriggeredSendDataExtension** | The source data for a triggered email send. It's sendable and comes with Subscriber Key and email address fields. This is the template usually meant by an email-send data extension. |
| **B** | **SendLog** | Records each email send (job, list, batch and subscriber IDs and similar). It's a log, not a list you send to. |

**Plan once you pick (A unless you say otherwise):**
1. Create `MCP_Email_Send_Test` from the template you choose, in folder 49911… correction, folder **49889 (MCP_Test)**, with external key `MCP_Email_Send_Test`. The template supplies the standard fields. You can als

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
