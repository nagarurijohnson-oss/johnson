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
**Status:** blocked — Awaiting user confirmation: delete standard table JNOT_CreatedDate_0938_Filtered or rename filtered output

**Done this session**
- Confirmed JNOT_CreatedDate_0938_Filtered is standard DataExtension (not filtered), 0 rows, folder 49911
- Identified root cause: Marketing Cloud fixes table type at creation; API attempts to create filtered version returned 500 errors
- Proposed two paths forward: (1) delete standard table + create filtered in Email Studio, or (2) save filtered table under different name

**Open items**
- User confirmation: delete standard table JNOT_CreatedDate_0938_Filtered or provide alternative name for filtered output
- If delete confirmed: I delete table, then user creates filtered table in Email Studio (3 clicks)
- If delete confirmed: verify filtered table type, source, and 10-row count after Email Studio save
- Execute two-step method on JMC_Amateur_Chef_Filtered (Email Studio steps from previous session)
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Verify both filtered tables report correct row counts when complete

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows
- Filtered table API route /automation/v1/filters not workable; use Email Studio or SQL query instead
- Path forward: delete standard JNOT_CreatedDate_0938_Filtered and create filtered version in Email Studio (or rename to avoid delete)

**Blockers**
- User must confirm delete of standard table JNOT_CreatedDate_0938_Filtered before proceeding; deletion is permanent

**Next**
- User replies: 'Confirm delete' OR provides alternative name (e.g. JNOT_CreatedDate_0938_FDE)
- If delete confirmed: I delete standard table and confirm deletion
- If delete confirmed: user creates filtered table in Email Studio (Subscribers → Data Extensions → John_N_Orchestrate_Test → Filter → load JNOT_CreatedDate_0938_Filter → Save As JNOT_CreatedDate_0938_Filtered)
- If delete confirmed: I verify filtered table type, source, and row count (expect 10 rows: TEST-CONTACT-006 to 015)

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
You're right: `JNOT_CreatedDate_0938_Filtered` is a **standard** table, not a filtered one. I made it as step 1 of the two-step attempt. Step 2 was meant to link it to the filter, and that failed. I've just checked it again: the type is still `DataExtension`, it has 0 rows, and it's in folder 49911.

**Why it can't just be changed.** Marketing Cloud fixes a table's type when the table is created, so there's no setting or API call that turns a standard table into a filtered one. Getting a filtered table under this name means deleting this one and creating the filtered version in its place.

**What I can and can't do from here**
- **Delete the standard table:** I can do this. It's empty, so no data is lost, but deleting it is permanent.
- **Create the filtered table:** I haven't been able to. Four API attempts with different request formats all returned `500 Internal Server Error`. Trying a fifth time without a new approach would just repeat that. The saved filter `JNOT_CreatedDate_0938_Filter` (CreatedDate = 10/6/2026 9:38:48 AM) still exists and is ready to use.

**Proposed path**
1. **I delete** the standard table `JNOT_CreatedDate_0938_Filtered` (ID `a95b95c8-adc1-f111-a5e6-5cba2

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
