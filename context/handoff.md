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
**Status:** waiting — Build plan ready for AUTO_Orchestrate_Full_Test. Awaiting 4 user decisions before creation.

**Done this session**
- Discovered folder 32393 (my automations) and source tables John_N_Orchestrate_Test (15 rows) and John_Mike_Customers (5 rows)
- Located csvUpload.csv in Enhanced FTP Import folder
- Designed 7-step automation with SQL Query, Data Copy, Import File, Data Extract, File Transfer, Script, and Send Email
- Planned 5 new test tables in folder 49911

**Open items**
- User chooses test recipient: (a) internal address OR (b) leave table empty
- User chooses schedule state: (a) turn on now OR (b) save paused for manual test run
- User chooses email content: create new test email OR reuse existing ORCH_TEST Welcome 1
- User confirms: proceed with creation of tables, activities, and automation

**Decisions**
- AUTO_Daily_Data_Load: switch from 7:00 AM IST schedule to file-triggered model
- Trigger source: Enhanced FTP Import folder, file queuing on
- Avoid csvUpload.csv as trigger file name (conflict with AUTO_Daily_Import)
- New automation AUTO_Orchestrate_Full_Test: daily 9:00 AM IST, folder 32393, 7 sequential steps
- Email send classification: Default Transactional (no unsubscribe/footer required)
- Data Copy implemented as Import activity with table source (not separate activity type)

**Blockers**
- None

**Next**
- User provides answer to question 1: test recipient choice and address if (a)
- User provides answer to question 2: schedule state (a) or (b)
- User provides answer to question 3: new email or reuse existing
- User confirms proceed with creation
- Create 5 test tables and load audience row if applicable
- Create email and 7 activities, build automation, read back all items to verify

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `f203b158-e2aa-4e90-b9af-ee68c9f98be8` |
**In its own words (excerpt):**
Discovery is done. Below is the build plan with real IDs from your tenant. Nothing has been created yet. I need four answers from you before I create anything.

## What I found
- **Folder 32393** is the Automation Studio folder "my automations". Your other `AUTO_*` automations are in it too.
- **John_N_Orchestrate_Test** has 15 rows. Fields: ContactKey (key), Name, Email, phone, CreatedDate.
- **John_Mike_Customers** has 5 rows. Fields: ContactKey (key), FirstName, Email, CreatedDate, Bio.
- **csvUpload.csv** is in the Enhanced FTP Import folder. Two imports read it successfully today at 09:29, and they don't delete the file, so it should still be there. I'll use it for the Import File test.

## Proposed automation: `AUTO_Orchestrate_Full_Test`
It goes in folder 32393, runs daily at 9:00 AM IST (India Standard Time), and has one activity per step so the steps run one after another:

| Step | Activity type | Activity name | What it does |
|---|---|---|---|
| 1 | SQL Query | `SQL_FullTest_Combine_Sources` | Combines both source tables, tagged by source, and overwrites `TEST_FullTest_SQL_Output` |
| 2 | Data Copy | `IMP_FullTest_DataCopy_JMC` | Copies `John_Mike_Customers` into `TEST_

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
