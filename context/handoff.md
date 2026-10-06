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
**Status:** waiting — Awaiting user confirmation to import 5 sample rows into John_Mike_Customers via upsert

**Done this session**
- Verified CSV file structure and column mapping for 5 sample rows (JMC-0001 to JMC-0005) — no changes made

**Open items**
- User confirms or cancels upsert of 5 rows into John_Mike_Customers
- Read back all 5 rows from John_Mike_Customers to verify import succeeded
- User confirms template choice (A or B) for MCP_Email_Send_Test creation
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- User manually updates TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- Escalate persistent confirmation dialog issue to Orchestrate admin (blocking 10+ sessions)

**Decisions**
- Bio field: Text type, length 20 chars, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, and short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- MCP_Email_Send_Test: will be created in folder 49889 with external key MCP_Email_Send_Test — awaiting template selection
- CreatedDate will populate with GetDate() default on import (CSV column blank)

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks irreversible modal display (tenth+ session)
- Template choice (A or B) required before MCP_Email_Send_Test creation can proceed

**Next**
- User replies 'Confirm' or 'Cancel' to proceed with or stop the 5-row upsert
- If confirmed: read back all 5 rows to verify import succeeded
- User provides template choice (A or B) for MCP_Email_Send_Test
- Escalate confirmation dialog blocker to Orchestrate admin

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | GENERAL |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `d2c94a85-3812-4b81-aae6-58f251fc82a5` |
**In its own words (excerpt):**
I haven't imported anything yet. The upsert is blocked until you explicitly confirm it, and the confirmation pop-up it requires isn't available in this session.

**What it will do**
- **Target:** Data Extension `John_Mike_Customers`. It currently has 0 rows.
- **Rows:** 5 rows, matched on the primary key `ContactKey` (JMC-0001 to JMC-0005). Existing keys are updated and new keys are added.
- **Column mapping:**
  - `ContactKey` → `ContactKey`
  - `FirstName` → `FirstName`
  - `Email` → `Email`
  - `Bio` → `Bio`
  - `CreatedDate` → `CreatedDate`. The CSV values are blank, so I'll leave this column out and the field's default will fill in the import time. Tell me if you'd rather I send a specific date instead.

Reply **"Confirm"** and I'll run the import, then check that the 5 rows landed. Reply **"Cancel"** to stop.
<!-- orchestrate:session-state:end -->
