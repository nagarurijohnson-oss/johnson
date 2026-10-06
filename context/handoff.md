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
### Engagement state — 2026-10-06
**Status:** on track — Phone update planned for 3 contacts in John_N_Orchestrate_Test — awaiting user approval to proceed

**Done this session**
- Re-read all 5 rows in John_N_Orchestrate_Test to confirm current phone numbers
- Proposed 3 new test phone numbers matching existing format (127587 prefix)
- Built before → after table for user confirmation

**Open items**
- User approves or modifies the 3 planned phone number changes
- Execute phone number update via sfmc_bulk_upsert_data_extension_rows on TEST-CONTACT-001, 002, 003
- Read all 5 rows back and verify 3 new numbers saved, 2 unchanged
- User approves creation of Orchestrate_Random_DE DE with 4 fields (ID, Name, Email, Date)
- Create Orchestrate_Random_DE in folder 49911, read back to verify schema and 0 rows
- Enable confirmation tool in session — required to display IRREVERSIBLE dialog before CSV insert
- Display IRREVERSIBLE dialog for 5-row CSV insert into John_N_Orchestrate_Test

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID primary key, Name, Email, Date), not sendable, no Subscriber Key link
- Proposed update: TEST-CONTACT-001 12758759879→12758750001, TEST-CONTACT-002 12758759889→12758750002, TEST-CONTACT-003 12758759332→12758750003

**Blockers**
- Confirmation tool not available — platform/admin setting blocks IRREVERSIBLE modal display

**Next**
- User confirms or modifies the 3 proposed phone numbers
- Execute upsert on John_N_Orchestrate_Test with new phone values
- Read back all 5 rows to verify changes persisted correctly

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `dbc33f2a-5193-4665-918d-f4285692262b` |
**In its own words (excerpt):**
I've picked three new test numbers. They use the same 11-digit format and `127587` prefix as your existing ones, so each is easy to recognise. I haven't changed anything yet, and the current values below are from a read I just did.

**Planned update: John_N_Orchestrate_Test, Phone field only**

| ContactKey | Name | Current Phone | → New Phone |
|---|---|---|---|
| TEST-CONTACT-001 | John Smith | 12758759879 | **12758750001** |
| TEST-CONTACT-002 | Sarah Johnson | 12758759889 | **12758750002** |
| TEST-CONTACT-003 | Michael Brown | 12758759332 | **12758750003** |

**What happens:**
- **One Marketing Cloud update** on these 3 rows, matched on ContactKey. Name, Email and CreatedDate stay as they are.
- **TEST-CONTACT-004 and 005** won't be touched.
- **The update overwrites the old numbers.** The current values are listed above, so you can put them back later if you need to.
- **Afterwards I'll read all 5 rows back** to check the 3 new numbers saved and the other 2 didn't change.
- **John filter** (001, 002) and **Segment 0** (003) are built from this table, so they'll show the new numbers after their next refresh.

**Proceed with these numbers?** If you'd like different ones, send t

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
