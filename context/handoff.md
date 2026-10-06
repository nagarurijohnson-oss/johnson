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
**Status:** at risk — Filtered table creation blocked by 500 errors; two-step retry proposed with risk of orphaned table

**Done this session**
- Third API attempt confirmed same 500 Internal Server Error
- Root cause identified: prior attempts created filter activity without pre-existing destination table
- Two-step retry strategy designed based on working example Filtered_DE_Test_Ashwin

**Open items**
- Execute two-step retry: create standard table JMC_Amateur_Chef_Filtered, then link via filter activity
- Verify filtered table type is FilteredDataExtension and contains JMC-0005 (Lucas)
- User creates filtered table in Email Studio if API retry fails (fallback)
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Two-step creation: table first, then filter activity with destinationObjectId
- Filtered table named JMC_Amateur_Chef_Filtered to avoid overwrite conflict

**Blockers**
- FilteredDataExtension creation via single-step POST /automation/v1/filters returns 500 Internal Server Error; root cause now identified as missing pre-created destination table

**Next**
- Await user reply: 'Proceed' or 'Proceed, use a test name'
- If Proceed: create table JMC_Amateur_Chef_Filtered, then POST filter activity with destinationObjectId
- If Proceed, use a test name: create table JMC_Amateur_Chef_Filtered_TEST, then link and verify before renaming
- Verify result reports type FilteredDataExtension and row count includes JMC-0005

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
Still not created: the third attempt returned the same `500 Internal Server Error`. The filtered table `JMC_Amateur_Chef_Filtered` doesn't exist yet, and nothing partial was left behind.

**What I found this time.** The working example `Filtered_DE_Test_Ashwin` was built in two steps. Its table was created at 05:18:32.777, and its filter activity 0.2 seconds later at 05:18:33.01, linked to that table through `destinationObjectId`. Each of my attempts asked the filter activity to create the table itself. That is the most likely reason they fail.

**Proposed two-step retry**
1. **Create the table:** `sfmc_create_data_extension` with name and key `JMC_Amateur_Chef_Filtered` in folder 49911, using the same 5 fields as the source (ContactKey as primary key, FirstName, Email, CreatedDate, Bio), not sendable.
2. **Link it:** `sfmc_rest_create` POST `/automation/v1/filters` with `destinationObjectId` set to the new table, `filterDefinitionId` = `2a430961-…`, `sourceObjectId` = `John_Mike_Customers`, and folder 49102, as in the example.
3. **Check:** read the table back and confirm it reports type `FilteredDataExtension` and contains JMC-0005 (Lucas).

**The risk.** If step 2 still fails, o

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
