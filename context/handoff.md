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
**Status:** blocked — Folder 49911 verified: 3 DEs, 8 rows total. Orchestrate_Random_DE creation awaits user approval.

**Done this session**
- Verified folder 49911 contains John_N_Orchestrate_Test (5 rows), John filter (2 rows), John_N_Orchestrate_Test Segment 0 (1 row)
- Confirmed Orchestrate_Random_DE does not yet exist

**Open items**
- User approves creation of Orchestrate_Random_DE DE with 4 fields (ID, Name, Email, Date)
- Create Orchestrate_Random_DE in folder 49911, read back to verify schema and 0 rows
- Enable confirmation tool in session — required to display IRREVERSIBLE dialog before CSV insert
- Display IRREVERSIBLE dialog for 5-row CSV insert into John_N_Orchestrate_Test
- User clicks Confirm in modal
- Execute sfmc_bulk_upsert_data_extension_rows for 5 CSV rows
- Read rows back and verify all 5 match CSV with CreatedDate populated
- Report final import counts: CSV rows, inserted, rejected, rejection reasons

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID primary key, Name, Email, Date), not sendable, no Subscriber Key link

**Blockers**
- User approval required before creating Orchestrate_Random_DE
- Confirmation tool not available — platform/admin setting blocks IRREVERSIBLE modal display

**Next**
- User replies 'proceed' to create Orchestrate_Random_DE
- Create DE and read back to verify schema and 0 rows
- Raise with Orchestrate admin: enable confirmation tool for next BUILD session

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `dbc33f2a-5193-4665-918d-f4285692262b` |
**In its own words (excerpt):**
The "John Orchestrate Test" folder (category 49911) has **3 Data Extensions** with **8 rows** between them. I only read data and changed nothing.

### 1. John_N_Orchestrate_Test: standard Data Extension, 5 rows
Key: `John_N_Orchestrate_Test` · Primary key: ContactKey

| ContactKey | Name | Email | Phone | CreatedDate |
|---|---|---|---|---|
| TEST-CONTACT-001 | John Smith | john.smith@example.com | 12758759879 | 10/6/2026 3:30:11 PM |
| TEST-CONTACT-002 | Sarah Johnson | sarah.johnson@example.com | 12758759889 | 10/6/2026 3:30:11 PM |
| TEST-CONTACT-003 | Michael Brown | michael.brown@example.com | 12758759332 | 10/6/2026 3:30:11 PM |
| TEST-CONTACT-004 | David Wilson | david.wilson@example.com | 12758759454 | 10/6/2026 3:30:11 PM |
| TEST-CONTACT-005 | Emily Davis | emily.davis@example.com | 12758759667 | 10/6/2026 3:30:11 PM |

### 2. John filter: filtered Data Extension, 2 rows
This is built from John_N_Orchestrate_Test.

| ContactKey | Name | Email | Phone | CreatedDate |
|---|---|---|---|---|
| TEST-CONTACT-001 | John Smith | john.smith@example.com | 12758759879 | 10/6/2026 3:30:11 PM |
| TEST-CONTACT-002 | Sarah Johnson | sarah.johnson@example.com | 12758759889 | 10/6/2026 3:

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
