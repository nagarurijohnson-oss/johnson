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
**Status:** on track — CSV validated, DE confirmed live, ready to import 5 rows. Awaiting proceed signal.

**Done this session**
- Verified DE John_N_Orchestrate_Test live in Salesforce org (ID 2c6c5dc5-…e778)
- Validated CSV: 5 rows, UTF-8 clean, header matches mapping, all ContactId and Email values well-formed and unique

**Open items**
- Import 5 CSV rows via sfmc_bulk_upsert_data_extension_rows
- Verify all 5 rows inserted with CreatedDate filled by GetDate() default
- Report final counts: CSV rows, inserted, rejected, and any rejection reasons

**Decisions**
- DE type: Standard, folder: Data Extensions (top level, 32375), Business Unit: MID 546010305
- Fields: ContactId (Text 50, nullable), Email (EmailAddress 254, required), CreatedDate (Date, required, GetDate() default)
- Not sendable, no Subscriber Key relationship
- Import method: upsert (insert-only in this case, no primary key, DE empty)
- Undo method: delete the 5 test rows

**Blockers**
- None

**Next**
- User confirms: proceed with import
- Execute sfmc_bulk_upsert_data_extension_rows for 5 rows (ContactId, Email only)
- Read rows back and verify all 5 match CSV with CreatedDate populated
- Report final import counts and any rejections

**Checked live on 2026-10-05:** the Salesforce org
### Last session — 2026-10-05
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `4248a4b9-0bc3-46fe-8666-2aeccb7b0147` |
**In its own words (excerpt):**
I've finished the checks before the import. Nothing has been written yet.

**The Data Extension (checked live):** `John_N_Orchestrate_Test` (ID `2c6c5dc5-…e778`) is in the top-level Data Extensions folder. It has the same 3 fields as before: `ContactId` Text(50) nullable, `Email` EmailAddress(254) required, `CreatedDate` Date required with the `GetDate()` default. It has **0 rows** right now.

**CSV validation: all 5 rows pass.**

| Check | Result |
|---|---|
| Encoding | Decodes as strict UTF-8. No byte-order mark, line endings are LF only, every character is plain ASCII (which is valid UTF-8) |
| Header | `ContactId,Email`, which matches the mapping exactly. No CreatedDate column |
| Data rows | **5** |
| ContactId | All present, all 16 characters (limit is 50), no duplicates |
| Email | All present and well-formed (`name@domain.tld`), 22–25 characters (limit is 254), no duplicates |

| Row | ContactId | Email |
|---|---|---|
| 1 | TEST-CONTACT-001 | john.smith@example.com |
| 2 | TEST-CONTACT-002 | sarah.johnson@example.com |
| 3 | TEST-CONTACT-003 | michael.brown@example.com |
| 4 | TEST-CONTACT-004 | david.wilson@example.com |
| 5 | TEST-CONTACT-005 | emily.davis@example.com |

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
