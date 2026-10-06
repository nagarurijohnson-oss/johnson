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
**Status:** blocked — 5-row upsert to John_Mike_Customers blocked by confirmation dialog unavailable in BUILD — recurring platform issue, 3 sessions

**Done this session**
- Verified John_Mike_Customers still has 0 rows (live check)
- Confirmed all 5 CSV rows (JMC-0001 to JMC-0005) are mapped and ready
- Validated Bio field has no length limit, default "No Biography is Available here" won't affect load

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
- Confirmation dialog unavailable in BUILD session — platform requires irreversible modal click before upsert executes (recurring: 3 sessions)

**Next**
- Admin escalation: enable confirmation pop-up for Marketing Cloud writes in BUILD sessions
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
I didn't load the rows, so there was nothing to verify. `John_Mike_Customers` still has **0 rows**; I checked that live just now.

**Why:** the platform counts this upsert as irreversible. It only runs after you click **Confirm** on a pop-up headed "IRREVERSIBLE". The tool that raises that pop-up isn't available in this session, so the call was stopped before it wrote anything. I won't get around the check, and a typed "yes" in chat doesn't count. This is the third session in a row to hit this, so it's a platform setup problem, not something wrong with your data.

**What's checked and ready:**

| Field | Type in the Data Extension | From the CSV |
|---|---|---|
| `ContactKey` (primary key) | Text, max 50 | JMC-0001 to JMC-0005 |
| `FirstName` | Text, max 50 | Aarav, Priya, Daniel, Meera, Lucas |
| `Email` | Email address | 5 `@example.com` addresses |
| `Bio` | Text | longest value is 17 characters ("Coffee enthusiast") |
| `CreatedDate` | Date, defaults to `GetDate()` | left out of the payload, as you asked, so the default fills it |

The table is empty, so this load would add 5 new rows and overwrite nothing.

One mismatch with the earlier session's notes: they recorded `Bio` as 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
