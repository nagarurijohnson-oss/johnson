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
**Status:** blocked — Awaiting user choice (a/b/c) on empty filtered table JNOT_CreatedDate_0938_Filtered; 10 matching rows confirmed in source.

**Done this session**
- Verified John_N_Orchestrate_Test contains 15 rows: TEST-CONTACT-001–005 (3:30:11 PM) and TEST-CONTACT-006–015 (9:38:48 AM)

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
- Empty table JNOT_CreatedDate_0938_Filtered blocks Email Studio save under same name; user must choose delete, query fill, or rename

**Next**
- Await user reply: (a) confirm delete empty table, (b) create SQL query to populate it, or (c) provide alternative table name
- If (a): delete table, then in Email Studio open John_N_Orchestrate_Test → Filter → load JNOT_CreatedDate_0938_Filter → Save As JNOT_CreatedDate_0938_Filtered
- If (b): create SQL query writing 10 matching rows into JNOT_CreatedDate_0938_Filtered
- If (c): save Email Studio filtered table under new name (e.g. JNOT_CreatedDate_0938_FDE)

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
`John_N_Orchestrate_Test` currently has **15 rows**.

- **TEST-CONTACT-001 to 005 (5 rows):** CreatedDate is 10/6/2026 3:30:11 PM
- **TEST-CONTACT-006 to 015 (10 rows):** CreatedDate is 10/6/2026 9:38:48 AM

That's the same count as earlier in this session, so nothing has been added or removed.

The empty `JNOT_CreatedDate_0938_Filtered` table is still waiting on your choice of (a), (b) or (c) from my last message.

Sources: checked live: Marketing Cloud (row query on `John_N_Orchestrate_Test`) · not checked: nothing
<!-- orchestrate:session-state:end -->
