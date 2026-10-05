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
**Status:** done — DE John_N_Orchestrate_Test recreated in top-level folder, spec-compliant, live and searchable

**Done this session**
- Recreated John_N_Orchestrate_Test in top-level Data Extensions folder (32375)
- Verified new DE matches original spec: not sendable, no Subscriber Key relationship
- Confirmed DE is visible in folder listing, name search, and External Key lookup
- Validated all three required fields with correct types, lengths, and defaults

**Open items**
- None

**Decisions**
- DE type: Standard, folder: Data Extensions (top level, 32375), Business Unit: MID 546010305
- Fields: ContactId (Text 50, nullable), Email (EmailAddress 254, required), CreatedDate (Date, required, GetDate() default)
- Not sendable, no Subscriber Key relationship
- New DE ID: 2c6c5dc5-e8c0-f111-a5e6-5cba2c19e778

**Blockers**
- None

**Next**
- User verifies DE is now visible in their Marketing Cloud interface
- If still not visible: confirm business unit is MID 546010305 and hard-refresh browser

**Checked live on 2026-10-05:** the Salesforce org
### Last session — 2026-10-05
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `4248a4b9-0bc3-46fe-8666-2aeccb7b0147` |
**In its own words (excerpt):**
I've recreated `John_N_Orchestrate_Test` in the top-level **Data Extensions** folder, so it shows in the main list without opening a subfolder. I read it back five ways and everything matches your spec.

**What happened to the first one:** it was deleted after my last check. Its ID returns "not found" and its External Key no longer matches anything, so the name and key were free to reuse.

**The new Data Extension:**

| Property | Value |
|---|---|
| Name | `John_N_Orchestrate_Test` |
| External Key | `John_N_Orchestrate_Test` |
| Data Extension ID | `2c6c5dc5-e8c0-f111-a5e6-5cba2c19e778` (new, different from the deleted one) |
| Folder | **Data Extensions** (the top level, folder 32375) |
| Business Unit | MID 546010305 |
| Sendable / Subscriber Key relationship | No / none |
| Rows | 0 |

| # | Field | Type | Length | Nullable | Primary Key | Default |
|---|---|---|---|---|---|---|
| 1 | `ContactId` | Text | 50 | Yes | No | none |
| 2 | `Email` | EmailAddress | 254 | No | No | none |
| 3 | `CreatedDate` | Date | — | No | No | `GetDate()` |

**How I checked it shows in the list:**
- **Folder listing:** it's the newest of the 33 DEs in the top-level folder, so it appears first.
- *

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
