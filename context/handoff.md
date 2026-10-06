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
**Status:** blocked — 5th attempt: confirmation dialog still unavailable in BUILD. John_Mike_Customers remains at 0 rows. Manual import or admin escalation requi…

**Done this session**
- Verified John_Mike_Customers exists in folder 49911 with 5 fields and 0 rows (live check)

**Open items**
- Admin enables confirmation pop-up for Marketing Cloud writes in BUILD sessions
- OR user imports 5 rows manually via Email Studio → Subscribers → Data Extensions → John_Mike_Customers → Import
- Read back all 5 rows from John_Mike_Customers to verify import succeeded
- User confirms template choice (A or B) for MCP_Email_Send_Test creation
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- User manually updates TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify

**Decisions**
- Bio field: Text type, no length limit, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, and short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- MCP_Email_Send_Test: will be created in folder 49889 with external key MCP_Email_Send_Test — awaiting template selection
- CreatedDate will populate with GetDate() default on import (CSV column blank)

**Blockers**
- Confirmation dialog unavailable in BUILD session — platform requires irreversible modal click before upsert executes (5 consecutive sessions blocked)

**Next**
- Admin escalation: enable confirmation pop-up for Marketing Cloud writes in BUILD sessions (recurring blocker across 5 sessions)
- User option: import 5 rows manually via Email Studio → Subscribers → Data Extensions → John_Mike_Customers → Import and report completion
- Once import confirmed: read back all 5 rows to verify success
- User provides template choice (A or B) for MCP_Email_Send_Test creation

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `fbfbb63f-a609-4058-ba8f-dde5306290a3` |
**In its own words (excerpt):**
I checked the Data Extension live. `John_Mike_Customers` exists in folder 49911 and has **0 rows**. It has 5 fields: `ContactKey` (the primary key, required), `FirstName`, `Email`, `CreatedDate` (fills in automatically with today's date) and `Bio`.

**What I plan to insert:** 5 new rows, using one bulk upsert call into `John_Mike_Customers`.

| ContactKey | FirstName | Email | Bio |
|---|---|---|---|
| JMC-0001 | Aarav | aarav.sample@example.com | Loves hiking |
| JMC-0002 | Priya | priya.sample@example.com | Coffee enthusiast |
| JMC-0003 | Daniel | daniel.sample@example.com | Weekend cyclist |
| JMC-0004 | Meera | meera.sample@example.com | Avid reader |
| JMC-0005 | Lucas | lucas.sample@example.com | Amateur chef |

- Every name, email and key is different. The emails use `example.com`, which can't receive mail.
- `CreatedDate` is left blank so it fills in with today's date.
- The table is empty, so nothing gets overwritten. The Data Extension isn't sendable, so no email goes out.

**Tool call I'll make:** Marketing Cloud bulk upsert on Data Extension `4cac233d-86c1-f111-a5e6-5cba2c19e778` with the 5 rows above. Afterwards I'll read the rows back to check all 5 arrived.

**One t

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
