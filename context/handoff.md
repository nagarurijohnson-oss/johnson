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
**Status:** waiting — Two-step filtered table method ready; awaiting user choice on CreatedDate filter condition (1/2/3) and approval to proceed

**Done this session**
- Analyzed John_N_Orchestrate_Test: 15 rows, 5 fields, CreatedDate stored in seconds
- Identified 10 rows with CreatedDate 9:38:48 AM (TEST-CONTACT-006 to 015)
- Confirmed 5 rows with CreatedDate 3:30:11 PM (TEST-CONTACT-001 to 005)
- Ruled out John_N_Orchestrate_Test Segment 0 (random-split segment, not filtered table)
- Designed three filter condition options for user decision

**Open items**
- User decision: proceed with filter condition (1) within-the-minute, (2) exactly 9:38:48 AM, or (3) whole day
- User approval: confirm table name or provide alternative
- Execute two-step retry on JMC_Amateur_Chef_Filtered: create standard table, then POST filter activity with destinationObjectId
- Execute two-step method on JNOT_CreatedDate_0938_Filtered with chosen condition
- Verify both filtered tables report type FilteredDataExtension and correct row counts
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Two-step creation: table first, then filter activity with destinationObjectId
- Filtered table named JMC_Amateur_Chef_Filtered to avoid overwrite conflict
- Recommended filter condition: (1) within-the-minute (9:38:00–9:39:00 AM) for 10 rows

**Blockers**
- FilteredDataExtension creation via single-step POST /automation/v1/filters returns 500 Internal Server Error; two-step method not yet tested

**Next**
- Await user reply: 'Proceed with (1)', (2), or (3)', optionally with alternative table name
- If approved: create JNOT_CreatedDate_0938_Filtered table, then POST filter activity with destinationObjectId
- In same pass: execute two-step method on JMC_Amateur_Chef_Filtered
- Verify both tables report type FilteredDataExtension and expected row counts

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I haven't created anything yet. The filter needs one decision from you, because no row is stamped exactly 9:38 AM. The API route for filtered tables is also still unproven.

**What I checked (read-only)**
- `John_N_Orchestrate_Test` (folder 49911) has 15 rows and 5 fields. `CreatedDate` is a Date field that stores seconds.
- **10 rows** have `CreatedDate` = 10/6/2026 **9:38:48 AM**: TEST-CONTACT-006 to 015 (Olivia Martinez to Daniel Lewis).
- The other **5 rows** (001 to 005) are 10/6/2026 3:30:11 PM.
- A filter of "equals 9:38:00 AM" would match **0 rows**, because of the 48 seconds.
- There's also a table called `John_N_Orchestrate_Test Segment 0`. It's a random-split segment, not a filtered table, so it doesn't meet this request.

**Open from your last request.** `JMC_Amateur_Chef_Filtered` still doesn't exist. Every API attempt to create a filtered table has returned `500 Internal Server Error`. The best lead so far is the two-step method: create the table first, then link the filter activity to it. That method hasn't been tested yet, and this table would use it too.

**Proposed plan**
1. **Saved filter** `JNOT_CreatedDate_0938_Filter` on `John_N_Orchestrate_Test`, using the co

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
