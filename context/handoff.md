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
**Status:** on track — Bio field verified on John_Mike_Customers. Ready to load 5 sample rows; awaiting user approval to proceed.

**Done this session**
- Verified John_Mike_Customers is empty (0 rows)
- Prepared 5 sample rows with Bio values (all ≤20 chars)
- Confirmed all ContactKey values unique, emails use example.com (safe for test)

**Open items**
- User approves sample row load or provides alternative names/emails/dates/bios
- Insert 5 rows into John_Mike_Customers and read back to verify
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

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks IRREVERSIBLE modal display (tenth+ session)
- Template choice (A or B) required before MCP_Email_Send_Test creation can proceed

**Next**
- User approves sample row load (or provides alternatives)
- Insert 5 rows into John_Mike_Customers, read back all 5 to verify
- User replies with template choice: A (TriggeredSendDataExtension) or B (SendLog) for MCP_Email_Send_Test
- Create MCP_Email_Send_Test from chosen template in folder 49889

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `4a65901d-f270-45ec-96fa-260777323520` |
**In its own words (excerpt):**
I checked `John_Mike_Customers` and it's still empty (0 rows). I haven't written anything yet. These are the 5 rows I'd insert:

| ContactKey | FirstName | Email | CreatedDate | Bio (max 20 chars) |
|---|---|---|---|---|
| JMC-0001 | Aarav | aarav.sample@example.com | 2026-09-01 | Loves hiking |
| JMC-0002 | Priya | priya.sample@example.com | 2026-09-08 | Coffee enthusiast |
| JMC-0003 | Daniel | daniel.sample@example.com | 2026-09-15 | Weekend cyclist |
| JMC-0004 | Meera | meera.sample@example.com | 2026-09-22 | Avid reader |
| JMC-0005 | Lucas | lucas.sample@example.com | 2026-09-29 | Amateur chef |

**About these rows:**
- Every Bio fits within the 20-character limit. The longest is "Coffee enthusiast" at 17 characters.
- The emails use `example.com`, which is reserved for testing, so nothing could ever go to a real inbox. The data extension also isn't sendable.
- All ContactKey values are unique. Because ContactKey is the primary key, running this again would update these 5 rows instead of adding duplicates.

**How I'll do it:**
1. Insert the 5 rows into `John_Mike_Customers` in one batch.
2. Read the rows back and confirm all 5 are there with the right values before I tell yo

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
