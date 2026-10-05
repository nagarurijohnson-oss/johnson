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
**Status:** blocked — BUILD failed: confirmation dialog unavailable + CSV not attached. Needs new session with both.

**Done this session**
- Verified DE schema matches expected mapping (ContactId, Email, CreatedDate)
- Confirmed DE still has 0 rows, ready for insert
- Identified two blockers preventing write execution

**Open items**
- User attaches John_N_test_records_UTF8.csv to next BUILD session
- Start new BUILD session with confirmation dialog tool loaded
- Display IRREVERSIBLE confirmation dialog (Confirm/Cancel)
- User clicks Confirm
- Execute sfmc_bulk_upsert_data_extension_rows for 5 rows (TEST-CONTACT-001 to 005)
- Read rows back and verify all 5 match CSV with CreatedDate populated
- Report final import counts: CSV rows, inserted, rejected, rejection reasons

**Decisions**
- DE type: Standard, folder: Data Extensions (32375), Business Unit: MID 546010305
- Fields: ContactId (Text 50, nullable), Email (EmailAddress 254, required), CreatedDate (Date, required, GetDate() default)
- Import method: upsert (insert-only, no primary key, DE empty)
- Confirmation gate required: irreversible bulk write must be gated by explicit user confirmation dialog
- Undo method: delete the 5 test rows manually post-import

**Blockers**
- Confirmation dialog unavailable in current session type — requires session with question tool loaded
- CSV file not attached to this session — cannot proceed without email addresses for 5 test rows

**Next**
- Attach John_N_test_records_UTF8.csv to next BUILD session
- Start new BUILD session with confirmation dialog capability enabled
- Display IRREVERSIBLE dialog with Confirm/Cancel buttons
- On user Confirm: run insert of 5 rows, read back all rows, verify CreatedDate filled, report counts

**Checked live on 2026-10-05:** the Salesforce org
### Last session — 2026-10-05
| | |
|---|---|
| Type | BUILD |
| Outcome | FAILED |
| Branch | `orchestrate/context` |
| Session | `8783e703-aab9-4180-986e-22bf5d910cae` |
**In its own words (excerpt):**
I haven't inserted anything. Two things are missing in this session, and either one alone would stop the write.

**1. I can't show the IRREVERSIBLE confirmation dialog.** The question tool that draws the Confirm/Cancel modal isn't available in this session, which is the same problem the last session hit. You asked for that dialog before any write. I won't swap in a typed "yes" in chat, and I won't set the confirmation flag myself.

**2. The CSV isn't attached to this session.** No attached file came through, and there's no `John_N_test_records_UTF8.csv` anywhere I can read. Last session's notes say it held TEST-CONTACT-001 to 005, but they don't record the email addresses. I'm not going to rebuild the rows from memory.

**What I checked just now (read-only), all fine:**
- **Target:** `John_N_Orchestrate_Test` (ID `2c6c5dc5-e8c0-f111-a5e6-5cba2c19e778`) is in folder 32375 and is not sendable.
- **Schema:** it matches your mapping.
  - `ContactId` is Text(50) and can be blank.
  - `Email` is EmailAddress(254) and required.
  - `CreatedDate` is a required Date with a default of `GetDate()`.
  - There's no primary key, so the write can only add rows.
- **Rows:** the DE has 0 rows. The 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
