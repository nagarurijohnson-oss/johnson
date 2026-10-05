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
**Status:** blocked — CSV valid & DE ready; confirmation dialog tool still unavailable — cannot proceed with insert

**Done this session**
- Validated CSV: 5 records (TEST-CONTACT-001 to 005), all headers and emails well-formed, no duplicates
- Confirmed DE schema matches mapping and has 0 rows
- Verified CreatedDate will auto-populate via GetDate() default

**Open items**
- Enable confirmation (question) tool in session — required to display IRREVERSIBLE dialog before write
- User clicks Confirm in modal
- Execute sfmc_bulk_upsert_data_extension_rows for 5 rows
- Read rows back and verify all 5 match CSV with CreatedDate populated
- Report final import counts: CSV rows, inserted, rejected, rejection reasons

**Decisions**
- DE type: Standard, folder: Data Extensions (32375), Business Unit: MID 546010305
- Fields: ContactId (Text 50, nullable), Email (EmailAddress 254, required), CreatedDate (Date, required, GetDate() default)
- Import method: upsert (insert-only, no primary key, DE empty)
- Confirmation gate required: irreversible bulk write must be gated by explicit user confirmation dialog
- Undo method: delete the 5 test rows manually post-import

**Blockers**
- Confirmation (question) tool not available in this session — platform/admin setting blocks IRREVERSIBLE modal display (second session in a row)

**Next**
- Raise with Orchestrate admin: enable confirmation tool for next BUILD session
- Start new BUILD session with confirmation dialog capability enabled
- Display IRREVERSIBLE dialog with Confirm/Cancel buttons
- On user Confirm: run insert of 5 rows, read back all rows, verify CreatedDate filled, report counts

**Checked live on 2026-10-05:** the Salesforce org
### Last session — 2026-10-05
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `e2c66d4c-e6b4-4b88-b068-193896c6617c` |
**In its own words (excerpt):**
I haven't written anything, and the Data Extension still has 0 rows. The CSV is valid, but I couldn't show the IRREVERSIBLE confirmation dialog, so the insert is stopped before it ran.

**CSV check: 5 records ready to insert**
- The headers are `ContactId,Email`, which match your mapping.
- **5 rows, all valid:**
  - None has an empty ContactId.
  - No value is longer than its field allows.
  - Every email is well-formed.
  - No ContactId or email appears twice.
- The rows are TEST-CONTACT-001 to 005, with emails from john.smith@ to emily.davis@example.com.

**Target check: `John_N_Orchestrate_Test`**
- ID `2c6c5dc5-…e778`, folder 32375, not sendable, currently **0 rows**.
- **Fields:**
  - `ContactId` is Text(50) and can be blank.
  - `Email` is EmailAddress(254) and required.
  - `CreatedDate` is a required Date with a default of `GetDate()`, so leaving it unmapped is fine.
- There's no primary key, so this write can only add rows. It won't update or delete anything, and the schema stays as it is.

**Why it stopped:** I called the insert tool without the confirmation flag. The platform blocked it, as it should, and said I must first raise the IRREVERSIBLE modal through the questi

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
