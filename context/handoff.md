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
**Status:** waiting — AUTO_Daily_Data_Load paused; step 1 now testOrchestrateMap import. Awaiting user file clarification.

**Done this session**
- Confirmed testOrchestrateMap import (step 1) writes 5 rows to John_Mike_Customers
- Searched Content Builder, all imports, file transfers, and tables for uploaded CSV
- Read John_Mike_Customers table: 5 rows, all dated 6 Oct (before import creation)

**Open items**
- User confirms trigger file name: AUTO_Daily_Data_Load_trigger.csv or custom
- User confirms match type: Exact name or Begins with
- User confirms activation: Yes or No
- User chooses resume timing: (a) now 7 AM, (b) pause-resume cycle, or (c) fix time/verify step 1
- Clarify actual CSV file: attach to chat OR name the table it was imported into
- Verify whether testOrchestrateMap has loaded user's file or contains older data

**Decisions**
- AUTO_Daily_Data_Load: switch from 7:00 AM IST schedule to file-triggered model
- Trigger source: Enhanced FTP Import folder, file queuing on
- Avoid csvUpload.csv as trigger file name (conflict with AUTO_Daily_Import)

**Blockers**
- Cannot access uploaded CSV (John_N_test_records_UTF8_b860c369-bbbb-47f5-abd1-2bd6cb490d02.csv) — not in Content Builder, FTP, or Safehouse

**Next**
- User attaches CSV to chat OR names the destination table for the import
- Verify testOrchestrateMap file contents and row count
- User provides three decisions (trigger name, match type, activation)
- User chooses resume timing option (a), (b), or (c)
- Convert AUTO_Daily_Data_Load to file-triggered and read back full automation

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I can't open `John_N_test_records_UTF8_b860c369-bbbb-47f5-abd1-2bd6cb490d02.csv`. It isn't anywhere I can read: it isn't in Content Builder, it isn't attached to this chat, and no import or file transfer refers to it by name. A name made of a file name plus a GUID is what Marketing Cloud gives a file uploaded from a computer through the Import wizard. It keeps that file in its internal Safehouse, and I have no tool that can read files there or on the FTP.

**The closest data I can read.** The import `testOrchestrateMap`, created today and now step 1 of `AUTO_Daily_Data_Load`, uses an uploaded file and writes to `John_Mike_Customers`. That table has 5 rows right now:

| ContactKey | FirstName | Email | CreatedDate (server time) | Bio |
|---|---|---|---|---|
| JMC-0001 | Aarav | aarav.sample@example.com | 10/6/2026 9:48:31 AM | Loves hiking |
| JMC-0002 | Priya | priya.sample@example.com | 10/6/2026 9:48:31 AM | Coffee enthusiast |
| JMC-0003 | Daniel | daniel.sample@example.com | 10/6/2026 9:48:31 AM | Weekend cyclist |
| JMC-0004 | Updated | meera.sample@example.com | 10/6/2026 9:48:31 AM | Avid reader |
| JMC-0005 | Lucas | lucas.sample@example.com | 10/6/2026 9:48:31 AM | Amateur

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
