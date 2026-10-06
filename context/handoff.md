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
**Status:** waiting — Standard table deleted; awaiting user to create filtered table in Email Studio (3 clicks)

**Done this session**
- Deleted standard table JNOT_CreatedDate_0938_Filtered (ID a95b95c8-adc1-f111-a5e6-5cba2c19e778, folder 49911, 0 rows)
- Confirmed deletion successful; external key name now free
- Verified saved filter JNOT_CreatedDate_0938_Filter still exists (ID a7dfb812-d8c6-493c-80d2-efe521ecd3ac)

**Open items**
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio from John_N_Orchestrate_Test + JNOT_CreatedDate_0938_Filter, replies 'done'
- Verify filtered table type (FilteredDataExtension), source (John_N_Orchestrate_Test), and row count (expect 10: TEST-CONTACT-006 to 015)
- Confirm date condition matches the 10 rows; if empty, switch to within-the-minute filter
- Execute two-step method on JMC_Amateur_Chef_Filtered (Email Studio steps from previous session)
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Verify both filtered tables report correct row counts when complete

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows
- Path forward: delete standard JNOT_CreatedDate_0938_Filtered and create filtered version in Email Studio

**Blockers**
- None

**Next**
- User creates filtered table in Email Studio: Subscribers → Data Extensions → John_N_Orchestrate_Test → Filter → JNOT_CreatedDate_0938_Filter → Save As JNOT_CreatedDate_0938_Filtered
- User replies 'done' when saved
- Verify filtered table type, source, and row count (expect 10 rows: TEST-CONTACT-006 to 015)

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I've deleted the standard table `JNOT_CreatedDate_0938_Filtered`. The filtered table doesn't exist yet. You'll need to create it in Email Studio, because every API attempt to create one has failed.

**What I did**
- **Before deleting:** I checked it was still the same table (ID `a95b95c8-adc1-f111-a5e6-5cba2c19e778`, folder 49911) and that it had 0 rows, so no data was lost.
- **Deleted it:** Marketing Cloud replied `Data Extension deleted.`
- **Checked afterwards:** a search for that external key now finds nothing, so the name is free.
- **Saved filter is still there:** `JNOT_CreatedDate_0938_Filter` (ID `a7dfb812-d8c6-493c-80d2-efe521ecd3ac`), with CreatedDate = 10/6/2026 9:38:48 AM.

**Your step in Email Studio (about 3 clicks)**
1. Go to **Email Studio → Subscribers → Data Extensions** and open `John_N_Orchestrate_Test` (folder 49911).
2. Click **Filter** and load the saved filter **`JNOT_CreatedDate_0938_Filter`**.
3. Click **Save As** and name it `JNOT_CreatedDate_0938_Filtered`.

Reply **"done"** when it's saved. I'll then check three things: that its type is `FilteredDataExtension`, that its source is `John_N_Orchestrate_Test`, and that it has 10 rows (TEST-CONTACT-006 to 0

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
