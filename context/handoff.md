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
**Status:** on track — PK constraint on ContactKey confirmed twice via insert rejection (error 71005). Table stable at 5 rows.

**Done this session**
- Re-ran insert-only test with duplicate ContactKey JMC-0001
- Confirmed primary key enforcement repeatable: error 71005 both runs
- Verified John_Mike_Customers unchanged: 5 rows, JMC-0001 still Aarav

**Open items**
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio UI
- Verify filtered table type, source, and row count (expect 10: TEST-CONTACT-006 to 015)
- Confirm date condition matches; if empty, switch to within-the-minute filter
- Execute two-step method on JMC_Amateur_Chef_Filtered
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Clarify: restore JMC-0004 FirstName from 'Updated' to 'Meera' or leave as-is

**Decisions**
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition (1): within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows
- API creation of filtered tables not viable; UI creation required
- Test PK constraint via insert-only route (not upsert) — CONFIRMED effective both runs
- Primary key ContactKey is enforced; insert-only rejects duplicates; upserts update instead

**Blockers**
- None

**Next**
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio (3 clicks)
- User clarifies: restore JMC-0004 FirstName to 'Meera' or leave 'Updated'
- Verify filtered table row count and date condition
- Execute two-step method on JMC_Amateur_Chef_Filtered
- Update TEST-CONTACT-001 phone in Contact Builder

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I ran the test again and Marketing Cloud rejected the duplicate `ContactKey` a second time. The table hasn't changed.

**What I sent:** one row through the insert-only route, using ContactKey **`JMC-0001`** (that key already exists) with FirstName `DuplicateTest`, Email `duplicate.test@example.com` and Bio `PK duplicate test`. The request ID is `c14fefe7-7142-4264-831f-75b57a8e1bbc`.

**What came back:** `status: Error`, error code **71005**:
> Violation of PRIMARY KEY constraint 'PK_C546010305_4cac233d-86c1-f111-a5e6-5cba2c19e778'. Cannot insert duplicate key in object 'C546010305.John_Mike_Customers'. The duplicate key value is (JMC-0001). The statement has been terminated.

**What I checked afterwards:** the table still has **5 rows**. JMC-0001 is still Aarav, aarav.sample@example.com, 10/6/2026 9:48:31 AM, "Loves hiking". The `DuplicateTest` row was never written, so there's nothing to clean up.

This matches the first run: the primary key on `ContactKey` is enforced, and an insert with an existing key fails with error 71005. Upserts work differently. They don't raise this error and update the existing row instead.

Row JMC-0004 still has FirstName **"Updated"**. If you want it

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
