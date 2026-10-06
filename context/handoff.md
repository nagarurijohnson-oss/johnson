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
**Status:** blocked — 5-row upsert to John_Mike_Customers blocked by irreversible confirmation pop-up unavailable in BUILD session

**Done this session**
- Confirmed John_Mike_Customers has 0 rows and is ready to receive 5 new rows
- Verified all CSV values fit their target fields
- Confirmed payload is mapped and ready to execute

**Open items**
- User clicks Confirm on platform's irreversible confirmation pop-up, then sends message to trigger upsert
- OR user imports 5 rows manually via Marketing Cloud Data Extension Import UI
- OR admin enables confirmation dialog for BUILD sessions
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
- Confirmation dialog unavailable in BUILD session — platform requires irreversible modal click before upsert executes (recurring blocker)

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
| Session | `bf54131c-6277-4134-a614-277bf4dd56cc` |
**In its own words (excerpt):**
I didn't load the rows. The Data Extension still has **0 rows**, which I confirmed with a read-back just now.

The platform treats this upsert as irreversible. It only runs after you click **Confirm** on a pop-up headed "IRREVERSIBLE". The tool that raises that pop-up isn't available in this session, so the call was blocked. I won't bypass the check, and a typed "yes" doesn't count as confirmation. This is the same blocker the previous session hit, so it's a recurring problem rather than a one-off.

**What I checked**
- **Data Extension:** `John_Mike_Customers` in folder 49911. It currently has 0 rows, so this load would add 5 new rows and overwrite nothing.
- **Primary key:** `ContactKey`, as you specified.
- **Fields:** `FirstName`, `Email` and `Bio` all exist, and every CSV value fits its field.
- **CreatedDate:** this is a Date field that fills itself in with the current date when it's left empty. All 5 CSV values are blank, so I left the column out of the payload. That way the field stamps the load time. Sending an empty string to a Date field can make the row fail.
- **The payload:** the 5 rows (JMC-0001 to JMC-0005) are mapped and ready. If the upsert can run, it will go fir

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
