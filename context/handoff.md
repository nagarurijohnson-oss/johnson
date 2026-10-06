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
**Status:** waiting — Awaiting approval to test primary key constraint on John_Mike_Customers via insert-only method

**Done this session**
- None

**Open items**
- User approves or modifies PK duplicate test plan (insert JMC-0001 with different values)
- Execute insert test and read async results to confirm PK rejection
- Verify John_Mike_Customers still has 5 rows and JMC-0001 unchanged if overwrite occurs
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio UI
- Verify filtered table type, source, and row count (expect 10: TEST-CONTACT-006 to 015)
- Confirm date condition matches; if empty, switch to within-the-minute filter
- Execute two-step method on JMC_Amateur_Chef_Filtered
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows
- API creation of filtered tables not viable; UI creation required
- Test PK constraint via insert-only route (not upsert) to avoid overwriting existing row

**Blockers**
- Marketing Cloud API has no endpoint for creating filtered tables; standard table endpoint lacks filter/source options; filter-activity route returns 500

**Next**
- User replies 'Proceed' or specifies alternate ContactKey for PK duplicate test
- Run insert test on John_Mike_Customers with JMC-0001 (different field values)
- Read async results and confirm PK rejection or restore row if overwritten
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio (3 clicks)

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I haven't inserted anything yet. This writes to a live table, so I need your go-ahead first.

**What I checked (read-only)**
- `ContactKey` is the primary key on `John_Mike_Customers` (`isPrimaryKey: true`, required, Text 50).
- The table has 5 rows, JMC-0001 to JMC-0005. The row I'd duplicate is **JMC-0001**: Aarav, aarav.sample@example.com, created 10/6/2026 9:48:31 AM, Bio "Loves hiking".

**Why the method matters.** Most of the row-write tools I have are *upserts*. Sending JMC-0001 through one of those wouldn't be rejected. It would just **overwrite Aarav's row**, and that would tell us nothing about the primary key. To actually test it, I'll use the insert-only route.

**Plan**
1. **Insert:** `sfmc_rest_create` POST `/data/v1/async/dataextensions/key:John_Mike_Customers/rows` with one row: ContactKey `JMC-0001`, FirstName `DuplicateTest`, Email `duplicate.test@example.com`, Bio `PK duplicate test`. The values are different on purpose, so we can tell if anything was overwritten.
2. **Read the outcome:** this route processes the request in the background, so I'll get the per-row result with `sfmc_rest_get` `/data/v1/async/{requestId}/results`. I expect a duplicate-key rejection 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
