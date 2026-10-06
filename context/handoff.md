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
**Status:** waiting — Awaiting confirmation pop-up or alternative import method to proceed with 5-row upsert into John_Mike_Customers

**Done this session**
- Confirmed CSV structure and column mapping are ready for import
- Clarified that typed confirmation does not satisfy platform's irreversible import requirement

**Open items**
- User clicks Confirm on platform's irreversible confirmation pop-up, then sends message to trigger upsert
- OR user imports 5 rows manually via Marketing Cloud Data Extension Import UI
- OR user starts Build session to enable write tools for upsert execution
- Read back all 5 rows from John_Mike_Customers to verify import succeeded
- User confirms template choice (A or B) for MCP_Email_Send_Test creation
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- User manually updates TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify

**Decisions**
- Bio field: Text type, length 20 chars, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, and short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- MCP_Email_Send_Test: will be created in folder 49889 with external key MCP_Email_Send_Test — awaiting template selection
- CreatedDate will populate with GetDate() default on import (CSV column blank)

**Blockers**
- Confirmation dialog unavailable in this session — platform requires irreversible modal click before upsert executes
- Template choice (A or B) required before MCP_Email_Send_Test creation can proceed

**Next**
- User clicks Confirm on irreversible pop-up in Marketing Cloud interface, then sends any message to trigger upsert
- If pop-up does not appear: user imports 5 rows manually via Data Extension Import, or starts Build session
- Once import completes: read back all 5 rows to verify success
- User provides template choice (A or B) for MCP_Email_Send_Test
- Escalate persistent confirmation dialog blocker to Orchestrate admin

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | GENERAL |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `d2c94a85-3812-4b81-aae6-58f251fc82a5` |
**In its own words (excerpt):**
I haven't imported anything. I can't run the upsert from your "confirm" message.

The import is classed as irreversible. The platform only releases it after you click Confirm on a dedicated confirmation pop-up (headed "IRREVERSIBLE"), and I can't raise that pop-up in this session. A typed confirmation doesn't satisfy it, and I won't bypass the check.

**What is ready to run**
- **Target:** Data Extension `John_Mike_Customers` (currently 0 rows).
- **Rows:** 5, matched on `ContactKey` (JMC-0001 to JMC-0005). Existing keys are updated and new keys are added.
- **Columns:** `ContactKey`, `FirstName`, `Email` and `Bio` map to the matching fields. I'm leaving out `CreatedDate` because the CSV values are blank, so the field's default fills in the import time.

**Ways to proceed**
- **Pop-up:** If a confirmation pop-up appears in your interface, click **Confirm** on it. Then send any message, and I'll run the upsert and check that the 5 rows landed.
- **Import yourself:** In Marketing Cloud, open the Data Extension and use **Import**. Choose the CSV, map the columns, and set **Add and Update**.
- **Build session:** Start a Build session. The write tools are loaded there, and I can run it 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
