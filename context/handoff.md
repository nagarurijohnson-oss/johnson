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
**Status:** blocked — Bulk insert blocked by platform safety check (7th time). Manual import via Email Studio required; admin escalation urgent.

**Done this session**
- Confirmed John_N_Orchestrate_Test still has 5 rows (TEST-CONTACT-001 to 005)
- Attempted bulk insert of 10 new rows; platform safety check blocked before execution
- Verified no table changes occurred; insert did not execute

**Open items**
- User imports 10 rows (TEST-CONTACT-006 to 015) manually via Email Studio → Subscribers → Data Extensions → John_N_Orchestrate_Test → Import
- User uploads CSV with 10 rows; maps ContactKey, Name, Email, phone; leaves CreatedDate unmapped
- User confirms import succeeded and table now has 15 total rows
- Admin enables confirmation pop-up for Marketing Cloud writes in BUILD sessions (7 consecutive blocks)
- User confirms template choice (A or B) for MCP_Email_Send_Test creation
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- User manually updates TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog

**Decisions**
- Bio field: Text type, no length limit, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, and short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- MCP_Email_Send_Test: will be created in folder 49889 with external key MCP_Email_Send_Test — awaiting template selection
- CreatedDate will populate with GetDate() default on import (CSV column blank)
- 10 new test contacts staged for John_N_Orchestrate_Test (TEST-CONTACT-006 to 015)

**Blockers**
- Confirmation dialog unavailable in BUILD session — platform requires irreversible modal click before upsert executes (7 consecutive sessions blocked)

**Next**
- User imports 10 rows via Email Studio manually using provided CSV
- User confirms import succeeded; table now has 15 rows
- Read back John_N_Orchestrate_Test to verify all 15 rows present
- Admin escalation: enable confirmation pop-up for Marketing Cloud writes in BUILD sessions (critical — 7 blocks)

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
The 10 rows were **not added**. `John_N_Orchestrate_Test` still has 5 rows (TEST-CONTACT-001 to 005).

I sent the insert again after your "confirm all", and the safety check stopped it before it ran, the same as last time. The check only accepts a click on Confirm in its own on-screen pop-up. A typed reply doesn't count, even an explicit one like yours. This session doesn't have the tool that shows that pop-up, so I can't get the click the check needs. I didn't set the override flag myself, because that would skip the check you're supposed to control.

**To add the rows yourself (about 2 minutes):**
1. Go to **Email Studio → Subscribers → Data Extensions → John_N_Orchestrate_Test → Import**.
2. Upload the CSV attached to this session. It has the 10 rows with ContactKey, Name, Email and phone.
3. Choose **Add and Update** and match the columns by name. Leave CreatedDate unmapped so it fills in automatically.
4. Tell me when it's done. I'll read the table back and check that it has 15 rows.

**To stop this happening again:** this is the seventh Marketing Cloud write blocked this way. An admin needs to turn on the confirmation pop-up for Build sessions. After that, a single click from

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
