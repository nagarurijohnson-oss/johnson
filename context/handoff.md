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
**Status:** on track — Table & query built, empty, awaiting user OK to run query & confirm Bio field width

**Done this session**
- Created John_Mike_Customers_Amateur_Chef table in folder 49911 with 5 fields, not sendable, 0 rows
- Created SQL Query Activity John_Mike_Customers_Amateur_Chef_Query in Automation Studio, validated, not yet run
- Confirmed table structure matches source except Bio is Text(100) instead of unlimited

**Open items**
- User confirms: run query now or widen Bio field first
- Run query to populate table with 1 row (JMC-0005, Lucas)
- Read table back after query run to confirm row populated
- Pick template (A or B) for MCP_Email_Send_Test creation
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text type, no length limit, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- CreatedDate populates with GetDate() default on import
- Query external key truncated by Marketing Cloud to John_Mike_Customers_Amateur_Chef_Que

**Blockers**
- None

**Next**
- User confirms: proceed with query run or widen Bio to unlimited first
- Run query to populate John_Mike_Customers_Amateur_Chef with 1 matching row
- Read table back to confirm row present and field types correct
- Proceed with MCP_Email_Send_Test template selection and creation

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
I built the table and the query, and read both back from Marketing Cloud to confirm they exist. The query **hasn't run yet**, so the new table is still empty.

**1. Table `John_Mike_Customers_Amateur_Chef`**
- Created in folder 49911 with external key `John_Mike_Customers_Amateur_Chef`. It's not sendable and has 0 rows.
- The 5 fields match the source: ContactKey is Text(50) and the primary key, FirstName is Text(50), Email is EmailAddress, and CreatedDate is Date.
- **One difference:** Bio came out as **Text(100)**, but in the source it has no length limit. The create call didn't keep "no limit" when I left the length out. Every current bio is short ("Amateur chef" is 12 characters), so the query will work. If the source ever has a bio over 100 characters that matches the filter, the run would fail. I can widen the field if you want that covered.

**2. SQL Query Activity `John_Mike_Customers_Amateur_Chef_Query`**
- Saved in the root **Query** folder in Automation Studio (folder 32395). It overwrites the new table each run, and Marketing Cloud validated the SQL with no errors.
- The query is `SELECT ContactKey, FirstName, Email, CreatedDate, Bio FROM [John_Mike_Customers] WHERE Bio

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
