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
**Status:** blocked — Two separate DE tasks blocked: CSV import awaits confirmation tool; new DE creation awaits user approval

**Done this session**
- Verified folder 'John Orchestrate Test' exists (category 49911)
- Confirmed 'Orchestrate_Random_DE' name and 'John_Mike' key are available
- Checked live Salesforce org — no conflicts found

**Open items**
- Enable confirmation tool in session — required to display IRREVERSIBLE dialog before CSV insert
- User approves creation of Orchestrate_Random_DE DE with 4 fields (ID, Name, Email, Date)
- Create Orchestrate_Random_DE in folder 49911, read back to verify schema and 0 rows
- Display IRREVERSIBLE dialog for 5-row CSV insert into John_N_Orchestrate_Test
- User clicks Confirm in modal
- Execute sfmc_bulk_upsert_data_extension_rows for 5 CSV rows
- Read rows back and verify all 5 match CSV with CreatedDate populated
- Report final import counts: CSV rows, inserted, rejected, rejection reasons

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID primary key, Name, Email, Date), not sendable, no Subscriber Key link

**Blockers**
- Confirmation (question) tool not available — platform/admin setting blocks IRREVERSIBLE modal display (third session in a row)
- User approval required before creating Orchestrate_Random_DE

**Next**
- Raise with Orchestrate admin: enable confirmation tool for next BUILD session
- User confirms: proceed with Orchestrate_Random_DE creation
- Create DE, read back to verify schema and 0 rows
- Start new BUILD session with confirmation dialog capability enabled
- Display IRREVERSIBLE dialog for CSV insert, execute on user Confirm, verify and report

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `dbc33f2a-5193-4665-918d-f4285692262b` |
**In its own words (excerpt):**
The checks passed and I haven't created anything yet.

**What I checked**
- **Folder:** "John Orchestrate Test" exists. It's a Data Extension folder with category ID **49911**, inside the "Data Extensions" folder (32375).
- **Name:** no Data Extension is called `Orchestrate_Random_DE` yet.
- **External key:** `John_Mike` isn't used by any other Data Extension.

**What I'll create** (one Marketing Cloud call to create a Data Extension)
- **Name / key:** `Orchestrate_Random_DE`, external key `John_Mike`, in folder 49911.
- **Settings:** a standard Data Extension. It won't be sendable and won't be linked to Subscriber Key.
- **Fields:**

| # | Field | Type | Length | Required | Primary Key |
|---|---|---|---|---|---|
| 1 | ID | Text | 50 | Yes | Yes |
| 2 | Name | Text | 100 | No | No |
| 3 | Email | EmailAddress | 254 | No | No |
| 4 | Date | Date | – | No | No |

- **What I won't touch:** I won't insert any records or change any existing Data Extension.
- **After creating it:** I'll read it back to confirm the name, key, ID and folder, check each field's type (making sure Date really saved as Date and not Text), confirm the primary key, and check that it has 0 rows.

This adds a new

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
