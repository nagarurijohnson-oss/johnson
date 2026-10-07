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
**Status:** waiting — Switched from scheduled to file-triggered model; awaiting user's three decisions on trigger file name, match type, and activation

**Done this session**
- Confirmed AUTO_Daily_Data_Load can switch from scheduled to file-triggered
- Identified AUTO_Daily_Import as working example using File Drop trigger
- Presented three-decision plan: trigger file name, match type, activation status

**Open items**
- User confirms trigger file name: AUTO_Daily_Data_Load_trigger.csv or custom name
- User confirms match type: Exact name or Begins with
- User confirms activation: Yes (run on next matching upload) or No (inactive until manual turn-on)
- Update AUTO_Daily_Data_Load from scheduled to file-triggered once decisions received
- Read back automation to verify trigger type, file name, folder, all 5 steps, and trigger state

**Decisions**
- AUTO_Daily_Data_Load: switch from 7:00 AM IST schedule to file-triggered model (replaces earlier chain-addition plan)
- Trigger source: Enhanced FTP Import folder, file queuing on
- Avoid csvUpload.csv as trigger file name (AUTO_Daily_Import already uses it; conflict risk if both activated)

**Blockers**
- None

**Next**
- User replies with all three decisions in one message (e.g., 'a, exact, yes')
- Once confirmed, update AUTO_Daily_Data_Load trigger and remove schedule
- Read back full automation configuration and confirm with user

**Checked live on 2026-10-07:** the Salesforce org
### Last session — 2026-10-07
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I haven't changed anything yet. The switch is doable, and your account already has a working example to copy: **`AUTO_Daily_Import`** runs on a File Drop trigger. It listens for `csvUpload.csv` in the Enhanced FTP **Import** folder, with file queuing on. Before I switch `AUTO_Daily_Data_Load`, there are a few things you should know and three decisions I need from you.

**What changes when it switches**
- **The daily schedule is removed.** It's paused right now and still set to 7:00 AM IST. Once switched, the automation runs only when a matching file lands on the FTP, so you won't need the 9:00 AM fix in Automation Studio any more.
- **None of the 5 steps reads the dropped file.** Steps 1 and 5 are SQL queries, and steps 2–4 export `John_N_Orchestrate_Test`. The file would only act as a "go" signal. That's fine if that's what you want, but it means the file's contents don't matter.
- **Avoid `csvUpload.csv` as the trigger file.** `AUTO_Daily_Import` already uses that name in the same folder. Its trigger is off at the moment, but if it's ever switched on, one upload would start both automations. A dedicated file name keeps them apart.
- I'm treating this as replacing my earlier quest

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
