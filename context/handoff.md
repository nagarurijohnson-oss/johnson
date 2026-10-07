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
### Engagement state — 2026-10-07
**Status:** waiting — Ready to test table-sourced import. Awaiting decision: new step 7 (a) or replace step 2 (b)?

**Done this session**
- None

**Open items**
- Decision: add ACT_DataCopy_Test as step 7 (a) or replace step 2 (b)
- Create ACT_DataCopy_Test via SOAP with table source John_Mike_Customers → TEST_FullTest_DataCopy
- Read ACT_DataCopy_Test back to verify table source saved (not file-based)
- Add to automation if it passes; keep automation Paused
- Run automation once to test all steps end-to-end
- Verify TEST_SQL_Output receives 5 rows after first run
- Add Send Email activity as final step manually in Automation Studio UI
- Restore step labels if needed

**Decisions**
- Cutoff filter: CreatedDate > '2026-10-06 09:38:48' (option B, 5 rows only)
- SQL Query step 6 position: at end of automation, after Script step 5
- Data Copy implemented as SQL query (table-to-table), not Import activity
- Send Email step deferred to manual UI creation due to API limitation
- Script logs row counts for SQL output and Data Copy only

**Blockers**
- Send Email activity cannot be created via API—manual UI step required
- Table-sourced import API behavior unknown—requires test to confirm Marketing Cloud accepts it

**Next**
- Reply (a) or (b) to confirm ACT_DataCopy_Test placement
- Create and read back ACT_DataCopy_Test to verify table source persists
- Proceed with automation test run once import validation is complete

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `f203b158-e2aa-4e90-b9af-ee68c9f98be8` |
**In its own words (excerpt):**
Checks are done and nothing has been created yet. Before I make changes I need your go-ahead, plus one decision.

## What I found
- **Source** `John_Mike_Customers` has 5 rows. **Target** `TEST_FullTest_DataCopy` has the same 5 fields (ContactKey as key, FirstName, Email, CreatedDate, Bio), so the columns can be matched by name.
- **The automation** has 6 steps and is still **Paused**, on its daily 9:00 AM IST schedule.
- **None of the 5 imports in this account reads from a table.** All of them, including `IMP_FullTest_DataCopy_JMC` from earlier, read a file from the Enhanced FTP. So I have no working example to copy.

## The risk
Earlier today Marketing Cloud's REST API rejected a table-sourced import with "File naming pattern cannot be blank". The SOAP import object does have a `SourceObject` property for a table source, but it also lists the file name and FTP location as required. I can't tell in advance whether Marketing Cloud will accept an import with no file. The only way to find out is to try it and read the result back.

## Plan
1. **Create `ACT_DataCopy_Test`** through SOAP: source `John_Mike_Customers`, destination `TEST_FullTest_DataCopy`, **Overwrite**, columns matched

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
