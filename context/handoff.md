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
**Status:** on track — SQL Query step 6 added to automation. TEST_SQL_Output table & ACT_SQL_Test query created & verified. Ready for first test run.

**Done this session**
- Created TEST_SQL_Output table (folder 49911, 5 fields, ContactKey primary key)
- Created ACT_SQL_Test query with cutoff '2026-10-06 09:38:48' (option B: 5 rows)
- Added ACT_SQL_Test as step 6 to AUTO_Orchestrate_Full_Test automation
- Verified all three objects read back correctly post-creation

**Open items**
- Run automation once to test all 6 steps end-to-end
- Verify TEST_SQL_Output receives 5 rows (TEST-CONTACT-001 to 005) after first run
- Verify TEST_FullTest_Script_Log row counts (step 5 runs before step 6, so won't count SQL output)
- Add Send Email activity as step 7 manually in Automation Studio UI
- Restore step labels if needed (SQL Query - Combine Sources, etc.)

**Decisions**
- Cutoff filter: CreatedDate > '2026-10-06 09:38:48' (option B, 5 rows only)
- SQL Query step 6 position: at end of automation, after Script step 5
- Data Copy implemented as SQL query (table-to-table), not Import activity
- Send Email step deferred to manual UI creation due to API limitation
- Script logs row counts for SQL output and Data Copy only

**Blockers**
- Send Email activity cannot be created via API—manual UI step required
- Step labels removed during automation update (side effect of 500 error retry)

**Next**
- Click Run Once on AUTO_Orchestrate_Full_Test to execute all 6 steps
- Check TEST_SQL_Output for 5 rows with correct ContactKey, Name, Email, phone, CreatedDate
- Review TEST_FullTest_Script_Log to confirm row counts logged by step 5
- Add Send Email activity manually in Automation Studio as step 7
- Restore step labels in automation if required by your workflow

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `f203b158-e2aa-4e90-b9af-ee68c9f98be8` |
**In its own words (excerpt):**
I created the table and the query and added the query to the automation as step 6. I read all three back to check them. Nothing has been run, so `TEST_SQL_Output` has 0 rows. When you next click Run Once, it should get 5 rows (TEST-CONTACT-001 to 005).

## The table `TEST_SQL_Output`
- It's in folder 49911 with the external key `TEST_SQL_Output`, and it can't be sent to.
- It has 5 fields: ContactKey (Text 50, primary key), Name (Text 50), Email (EmailAddress), phone (Phone) and CreatedDate. CreatedDate is a real Date field, not text.

## The query `ACT_SQL_Test`
- Query text: `SELECT ContactKey, Name, Email, phone, CreatedDate FROM [John_N_Orchestrate_Test] WHERE CreatedDate > '2026-10-06 09:38:48'`
- It writes to `TEST_SQL_Output` and **overwrites** it on every run.
- It passed Marketing Cloud's syntax check. It's saved in folder 32395, the same folder as your other query activities.

## The automation `AUTO_Orchestrate_Full_Test`
| Step | Activity | Target |
|---|---|---|
| 1 | SQL_FullTest_Combine_Sources | TEST_FullTest_SQL_Output |
| 2 | SQL_FullTest_DataCopy_JMC | TEST_FullTest_DataCopy |
| 3 | DX_FullTest_JNOT_Extract | export file |
| 4 | FT_FullTest_JNOT_Export | Enhanced

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
