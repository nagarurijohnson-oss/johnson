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
**Status:** blocked — Two-step filtered table method failed (500 error). Empty table created; awaiting user choice (a/b/c) to proceed.

**Done this session**
- Created saved filter JNOT_CreatedDate_0938_Filter (ID a7dfb812-…) on John_N_Orchestrate_Test, condition CreatedDate = 10/6/2026 9:38:48 AM
- Created empty table JNOT_CreatedDate_0938_Filtered (ID a95b95c8-…, folder 49911) with correct 5 fields and types
- Confirmed POST /automation/v1/filters with destinationObjectId returns 500 Internal Server Error; two-step method does not work

**Open items**
- User decision: (a) delete empty table and finish in Email Studio, (b) fill table with SQL query, or (c) save under different name
- Execute chosen path for JNOT_CreatedDate_0938_Filtered (expect 10 rows: TEST-CONTACT-006 to 015)
- Execute two-step method on JMC_Amateur_Chef_Filtered (Email Studio steps from previous session)
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Verify both filtered tables report correct row counts when complete

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows
- Filtered table API route /automation/v1/filters is not workable; use Email Studio or SQL query instead

**Blockers**
- POST /automation/v1/filters with destinationObjectId returns 500 Internal Server Error; filtered table creation via API not viable
- Empty table JNOT_CreatedDate_0938_Filtered blocks Email Studio save under same name; user must choose delete, query fill, or rename

**Next**
- Await user reply: (a) confirm delete empty table, (b) create SQL query to populate it, or (c) provide alternative table name
- If (a): delete table, then in Email Studio open John_N_Orchestrate_Test → Filter → load JNOT_CreatedDate_0938_Filter → Save As JNOT_CreatedDate_0938_Filtered
- If (b): create SQL query writing 10 matching rows into JNOT_CreatedDate_0938_Filtered
- If (c): save Email Studio filtered table under new name (e.g. JNOT_CreatedDate_0938_FDE)
- For JMC_Amateur_Chef_Filtered: apply Email Studio steps from previous session (no API route available)

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
The filtered table wasn't created. The two-step method failed with the same `500 Internal Server Error` as the earlier attempts. I created the saved filter, but the table that now exists is a plain, empty table, not a filtered one.

**Created and confirmed by reading back**
- **Saved filter `JNOT_CreatedDate_0938_Filter`** (ID `a7dfb812-d8c6-493c-80d2-efe521ecd3ac`). Its source is `John_N_Orchestrate_Test` and its condition is CreatedDate equals `10/6/2026 9:38:48 AM`, as you chose. The first create attempt was rejected because the description contained `/` and `:` ("Description cannot contain illegal characters"). The second attempt, with a plain-text description, worked.
- **Table `JNOT_CreatedDate_0938_Filtered`** (ID `a95b95c8-…`, folder 49911). It has the 5 source fields with the right types: CreatedDate is Date, ContactKey is the primary key. It is **type `DataExtension`, not `FilteredDataExtension`, and has 0 rows.**

**What failed**
- **Linking them:** `POST /automation/v1/filters` with `destinationObjectId` set to the new table, matching the working example field for field. It returned `500 Internal Server Error` (`errorcode: 0`). No filter activity was created; there are 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
