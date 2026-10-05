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
### Engagement state — 2026-10-05
**Status:** at risk — DE created & live in Orchestrate Test folder, but sendability was changed post-creation—spec mismatch needs clarification

**Done this session**
- Confirmed DE John_N_Orchestrate_Test exists live in Orchestrate Test folder (49107)
- Identified likely reasons DE not visible in user's list (subfolder depth, BU context, cache)
- Detected unintended change: DE now sendable with ContactId→Subscriber Key relationship

**Open items**
- Clarify whether sendability change (made by John at 12:04) was intentional or should be reverted
- Confirm user is viewing correct Business Unit (MID 546010305) and folder path
- Determine if sendability can be safely reverted if change was unintended

**Decisions**
- DE type: Standard, folder: Orchestrate Test (49107), fields: ContactId (Text 50), Email (EmailAddress 254, required), CreatedDate (Date, required, GetDate() default)
- Original spec: not sendable, no Subscriber Key relationship

**Blockers**
- DE sendability state now conflicts with original specification

**Next**
- User confirms whether sendability change was intended
- If unintended: check revert feasibility and apply if possible
- User verifies they're in correct BU and folder when searching for DE

**Checked live on 2026-10-05:** the Salesforce org
### Last session — 2026-10-05
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `4248a4b9-0bc3-46fe-8666-2aeccb7b0147` |
**In its own words (excerpt):**
The DE still exists. I just checked it live and it's in **Orchestrate Test** (folder 49107) alongside four other DEs. So the problem is where the UI is looking, not that the DE is missing. I also found a change to it since I created it, covered at the end.

## Likely reasons it's not in your list

**1. You're looking at the top-level list instead of the subfolder.** This is the most common cause. Clicking **Data Extensions** in Email Studio or Contact Builder shows only the DEs at the root of the folder tree. This DE is one level down. Expand **Data Extensions → Orchestrate Test** in the left-hand folder tree, or search for `John_N_Orchestrate_Test` with the search box at the top of the list.

**2. You're in a different Business Unit.** The integration created the DE in business unit **MID 546010305**, which is the enterprise (parent) BU. If your switcher in the top-right of Marketing Cloud shows a child BU, you won't see it. Switch to MID 546010305. DEs only appear across BUs if they're created under *Shared Data Extensions*, and this one wasn't.

**3. The page is showing an old list.** Folder lists can be cached from before the DE was created (11:59 server time). A hard refresh (

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
