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
**Status:** blocked — 4th consecutive upsert blocked by unavailable confirmation dialog in BUILD — admin escalation or manual import required

**Done this session**
- Verified John_Mike_Customers still has 0 rows (live check before and after attempt)
- Confirmed all 5 CSV rows ready for insert (JMC-0001 to JMC-0005)

**Open items**
- Admin enables confirmation pop-up for Marketing Cloud writes in BUILD sessions
- OR user imports 5 rows manually via Marketing Cloud Data Extension Import UI (Email Studio → Subscribers → Data Extensions → John_Mike_Customers → Import)
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
- Confirmation dialog unavailable in BUILD session — platform requires irreversible modal click before upsert executes (4 consecutive sessions blocked)

**Next**
- Admin escalation: enable confirmation pop-up for Marketing Cloud writes in BUILD sessions (recurring blocker)
- User option: import 5 rows manually via Marketing Cloud Data Extension Import UI and report completion
- Once import confirmed: read back all 5 rows to verify success
- User provides template choice (A or B) for MCP_Email_Send_Test creation

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `12629cfa-6d99-4ea3-abbd-184150d7d7d2` |
**In its own words (excerpt):**
The 5 rows were not inserted. `John_Mike_Customers` still has **0 rows**; I checked that live just before and after the attempt.

**Why it stopped:** the platform treats this write as permanent. It only runs after you click **Confirm** on a pop-up headed "IRREVERSIBLE". I can't raise that pop-up in this session, so the call was stopped before anything was written. A "yes" typed in chat doesn't count as that confirmation, and I won't skip the check. This is the fourth time in a row a write here has been stopped this way, which points to how this session type is set up, not to your data.

**The 5 rows I submitted:**

| ContactKey (primary key) | FirstName | Email | Bio |
|---|---|---|---|
| JMC-0001 | Aarav | aarav.sample@example.com | Loves hiking |
| JMC-0002 | Priya | priya.sample@example.com | Coffee enthusiast |
| JMC-0003 | Daniel | daniel.sample@example.com | Weekend cyclist |
| JMC-0004 | Meera | meera.sample@example.com | Avid reader |
| JMC-0005 | Lucas | lucas.sample@example.com | Amateur chef |

These come from your attached CSV. Every name, email and key is different, and `CreatedDate` is left out so its default (`GetDate()`) fills it in. The table is empty, so this woul

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
