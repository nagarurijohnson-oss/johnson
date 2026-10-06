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
**Status:** at risk — Saved filter created; filtered table API failed 500×2. User must finish in Email Studio (3 clicks).

**Done this session**
- Created saved filter JMC_Amateur_Chef_Filter (ID 2a430961-6ca1-430a-bb16-67c370b0f713) on John_Mike_Customers for Bio equals 'Amateur chef'
- Confirmed filter reads back correctly with source table and condition
- Attempted filtered table creation via POST /automation/v1/filters twice; both returned 500 Internal Server Error

**Open items**
- User creates filtered table JMC_Amateur_Chef_Filtered in Email Studio (Subscribers → Data Extensions → John_Mike_Customers → Filter → Save As)
- Verify filtered table type is FilteredDataExtension and contains JMC-0005 (Lucas)
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100) in new table; all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Attempt API creation of FilteredDataExtension before falling back to Email Studio manual creation
- New filtered table named JMC_Amateur_Chef_Filtered to avoid overwrite conflict with old query

**Blockers**
- FilteredDataExtension creation endpoint POST /automation/v1/filters returns 500 Internal Server Error; cause unknown (request format or service limitation)
- SOAP route blocked by Orchestrate tool limitation (cannot send nested DataFilter)

**Next**
- User completes filtered table creation in Email Studio (3 clicks as documented)
- User replies 'done' once saved
- Verify filtered table type, source, and row count (JMC-0005 present)
- Proceed to TEST-CONTACT-001 phone update and MCP_Email_Send_Test creation

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
The filtered table `JMC_Amateur_Chef_Filtered` was not created. I created the saved filter, but the call that should create the filtered table failed twice. You'll need to finish it in Email Studio, which takes about three clicks.

**Created and confirmed**
- **Saved filter `JMC_Amateur_Chef_Filter`** (ID `2a430961-6ca1-430a-bb16-67c370b0f713`). It is a filter on `John_Mike_Customers` for Bio equals "Amateur chef". Reading it back after creation confirmed the source table and the condition.

**What failed**
- **Creating the filtered table:** I tried this twice with `POST /automation/v1/filters`, which is the route the working example `Filtered_DE_Test_Ashwin` is built on. Both calls returned exactly: `500 Internal Server Error` (`errorcode: 0`).
- That error doesn't say whether my request was wrong or the service doesn't support this, and there's no documentation for this endpoint. I stopped after two tries rather than keep guessing.
- I also tried the SOAP route. It failed because Orchestrate's SOAP tool can't send the nested filter (`DataFilter is required for Create calls`). That's a gap in our tool, not a Marketing Cloud limitation.
- Neither failed call left a partial table or

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
