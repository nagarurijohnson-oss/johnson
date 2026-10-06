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
**Status:** at risk — John_N_Orchestrate_Test verified at 5 rows; 10 new rows staged for insert—platform safety check may block again.

**Done this session**
- Verified John_N_Orchestrate_Test has 5 existing rows (TEST-CONTACT-001 to 005)
- Staged 10 new test contacts (TEST-CONTACT-006 to 015) with names, emails, phone numbers

**Open items**
- Admin enables confirmation pop-up for Marketing Cloud writes in BUILD sessions
- OR user imports 5 rows manually via Email Studio → Subscribers → Data Extensions → John_Mike_Customers → Import
- Read back all 5 rows from John_Mike_Customers to verify import succeeded
- User confirms template choice (A or B) for MCP_Email_Send_Test creation
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Execute bulk insert of 10 rows into John_N_Orchestrate_Test; read back to verify 15 total rows
- User manually updates TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog

**Decisions**
- Bio field: Text type, no length limit, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, and short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- MCP_Email_Send_Test: will be created in folder 49889 with external key MCP_Email_Send_Test — awaiting template selection
- CreatedDate will populate with GetDate() default on import (CSV column blank)
- 10 new test contacts staged for John_N_Orchestrate_Test (TEST-CONTACT-006 to 015)

**Blockers**
- Confirmation dialog unavailable in BUILD session — platform requires irreversible modal click before upsert executes (5 consecutive sessions blocked, 6th attempt pending)

**Next**
- User confirms: proceed with bulk insert of 10 rows into John_N_Orchestrate_Test
- If insert succeeds: read back table to confirm 15 total rows
- If insert blocked again: user imports via Email Studio manually (CSV provided)
- Admin escalation: enable confirmation pop-up for Marketing Cloud writes in BUILD sessions

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
I checked `John_N_Orchestrate_Test`. It has **5 rows** right now (TEST-CONTACT-001 to 005) and 5 fields: ContactKey (primary key), Name, Email, phone, and CreatedDate (fills in automatically with today's date).

**The 10 rows I plan to add**

| ContactKey | Name | Email | phone |
|---|---|---|---|
| TEST-CONTACT-006 | Olivia Martinez | olivia.martinez@example.com | 12758759101 |
| TEST-CONTACT-007 | James Anderson | james.anderson@example.com | 12758759102 |
| TEST-CONTACT-008 | Sophia Thomas | sophia.thomas@example.com | 12758759103 |
| TEST-CONTACT-009 | Benjamin Taylor | benjamin.taylor@example.com | 12758759104 |
| TEST-CONTACT-010 | Ava Moore | ava.moore@example.com | 12758759105 |
| TEST-CONTACT-011 | Lucas Jackson | lucas.jackson@example.com | 12758759106 |
| TEST-CONTACT-012 | Mia White | mia.white@example.com | 12758759107 |
| TEST-CONTACT-013 | Henry Harris | henry.harris@example.com | 12758759108 |
| TEST-CONTACT-014 | Charlotte Clark | charlotte.clark@example.com | 12758759109 |
| TEST-CONTACT-015 | Daniel Lewis | daniel.lewis@example.com | 12758759110 |

**What I'll do once you confirm**
- **Add the rows:** one bulk insert of the 10 rows into `John_N_Orchestrate_Test`.

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
