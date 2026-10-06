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
**Status:** blocked — 5th consecutive upsert blocked by confirmation dialog. Manual import or admin escalation required.

**Done this session**
- Attempted bulk upsert of 5 rows into John_Mike_Customers
- Confirmed platform safety check blocked write (no confirmation dialog available)
- Verified Data Extension still at 0 rows post-attempt

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
- Admin escalation: enable confirmation pop-up for Marketing Cloud writes in BUILD sessions
- User option: import 5 rows manually via Email Studio → Subscribers → Data Extensions → John_Mike_Customers → Import using provided CSV
- Once import confirmed: read back all 5 rows to verify success and CreatedDate population
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
The 5 rows were not inserted. The platform blocked the write again, and `John_Mike_Customers` still has **0 rows**.

**What happened**
- I sent the bulk upsert with the 5 rows exactly as listed, with `CreatedDate` left out.
- The platform's safety check stopped it before anything reached Marketing Cloud. The write only runs after you click **Confirm** on an "IRREVERSIBLE" pop-up. I don't have a way to show you that pop-up in this session.
- Your "proceed" message doesn't count as that confirmation. The platform specifically requires the pop-up click, so I haven't tried to get around it or retried.
- I read the Data Extension back to check: it has 0 rows, so nothing was partly written.

This is the fifth session in a row where this write has been blocked the same way.

**Two ways to get the rows in**
1. **Import them manually (about 2 minutes).** Go to **Email Studio → Subscribers → Data Extensions → John_Mike_Customers → Import** and upload this CSV. Leave out the `CreatedDate` column so it fills in with today's date:
   ```
   ContactKey,FirstName,Email,Bio
   JMC-0001,Aarav,aarav.sample@example.com,Loves hiking
   JMC-0002,Priya,priya.sample@example.com,Coffee enthusiast
   JMC-0

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
