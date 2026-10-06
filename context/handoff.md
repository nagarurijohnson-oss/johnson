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
**Status:** on track — PK constraint on John_Mike_Customers confirmed via insert rejection (error 71005). Table intact, 5 rows.

**Done this session**
- Executed insert-only test with duplicate ContactKey JMC-0001
- Confirmed primary key enforcement: insert rejected with error 71005
- Verified John_Mike_Customers unchanged: 5 rows, JMC-0001 still Aarav

**Open items**
- User approves or modifies PK duplicate test plan — COMPLETED, test executed
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
- Test PK constraint via insert-only route (not upsert) — CONFIRMED effective
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
Marketing Cloud rejected the duplicate, and the table hasn't changed.

**Result**
- **Insert rejected.** The request finished with `resultStatus: Error`, error code **71005**:
  > Violation of PRIMARY KEY constraint 'PK_C546010305_4cac233d-86c1-f111-a5e6-5cba2c19e778'. Cannot insert duplicate key in object 'C546010305.John_Mike_Customers'. The duplicate key value is (JMC-0001).
- **Table unchanged.** It still has **5 rows**. JMC-0001 still reads Aarav, aarav.sample@example.com, 10/6/2026 9:48:31 AM, "Loves hiking". The test row `DuplicateTest` was never written, so nothing needs restoring.

So the primary key on `ContactKey` is enforced. An insert with an existing key fails with error 71005.

**Upserts behave differently.** The upsert tools (and the Import "Add and Update" mode) don't raise this error. They update the existing row instead. Only insert-only routes report the conflict.

**Separate thing I noticed.** Row **JMC-0004** has FirstName **"Updated"**, not a real name (email meera.sample@example.com). This test didn't touch that row because it only sent JMC-0001, so the value was probably left by an earlier test. Tell me if you want it set back to "Meera".

Sources: checked 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
