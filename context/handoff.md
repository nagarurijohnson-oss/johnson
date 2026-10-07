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
**Status:** blocked — Table-sourced import rejected by both APIs—requires UI workaround or design change

**Done this session**
- Confirmed John_Mike_Customers (5 rows) matches TEST_FullTest_DataCopy schema
- Tested table-sourced import via SOAP and REST—both rejected for missing file/FTP fields
- Verified AUTO_Orchestrate_Full_Test unchanged (6 steps, Paused)

**Open items**
- Decision: build Import File activity in UI (option 1) or accept step 2 SQL copy as final solution (option 2)
- If option 1: create step 7 Import File in Automation Studio UI with John_Mike_Customers table source
- If option 1: read back step 7 to verify table source persists without file/FTP in API view
- Run automation end-to-end test once import strategy is decided
- Verify TEST_SQL_Output receives 5 rows after first run
- Add Send Email activity as final step manually in Automation Studio UI
- Restore step labels if needed

**Decisions**
- Cutoff filter: CreatedDate > '2026-10-06 09:38:48' (5 rows only)
- SQL Query step 6 position: at end of automation, after Script step 5
- Data Copy implemented as SQL query (table-to-table), not Import activity
- Send Email step deferred to manual UI creation due to API limitation
- Script logs row counts for SQL output and Data Copy only

**Blockers**
- Marketing Cloud APIs require file name, file type, and FTP location for all imports—table-sourced imports cannot be created via SOAP or REST without file metadata
- Unknown whether Automation Studio UI can save table-sourced import in a way APIs expose without file/FTP fields

**Next**
- Choose option 1 (UI-built Import File step 7) or option 2 (keep step 2 SQL copy only)
- If option 1: build and save step 7 in Automation Studio UI, then read back to test API visibility
- If option 2: proceed directly to end-to-end automation test run

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `f203b158-e2aa-4e90-b9af-ee68c9f98be8` |
**In its own words (excerpt):**
I couldn't create `ACT_DataCopy_Test`. Marketing Cloud rejected a table-sourced import twice, through two different APIs, so nothing was created and step 7 wasn't added. The automation is unchanged and still Paused.

## What Marketing Cloud returned
**SOAP** (source `John_Mike_Customers`, destination `TEST_FullTest_DataCopy`, Overwrite, no file):
> ImportDefinition DestinationObjects was not specified in the request.
> ImportDefinition FileTransferLocation was not specified in the request.
> ImportDefinition FileSpec was not specified in the request.
> ImportDefinition FileType was not specified in the request.

The first line, "DestinationObjects", is my tool's fault. It dropped the nested source and destination table settings, the same problem it had with the Send Email setup. The other three lines are Marketing Cloud's own rules: it wants a file name, a file type and an FTP location.

**REST** (same settings, table as source):
> The following field is required: 'FileType'.
> The following field is required: 'FileTransferLocationId'.
> The following field is required: 'SendEmailNotification'.

Both APIs require a file and an FTP location for an import. I can't meet your "no CSV, 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
