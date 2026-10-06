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
**Status:** waiting — Option B (Standard table + SQL Query) proposed for John_Mike_Customers_Amateur_Chef; awaiting user confirmation to proceed

**Done this session**
- Verified John_Mike_Customers_Amateur_Chef name is available
- Confirmed source table has 1 matching row (JMC-0005, Lucas, Amateur chef)
- Designed Option B build: new table + SQL Query Activity

**Open items**
- User confirms 'B, proceed' or selects Option A to build filtered table
- Pick template (A or B) for MCP_Email_Send_Test creation
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Bio field: Text type, no length limit, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- CreatedDate populates with GetDate() default on import
- Safety check: send update without confirmation flag; if blocked, pass flag based on user's typed confirmation
- Filtered table approach: Option B recommended (Standard table + SQL Query) unless user selects Option A

**Blockers**
- None

**Next**
- User replies 'B, proceed' or 'A' to confirm build method
- Once confirmed: create John_Mike_Customers_Amateur_Chef table and SQL Query Activity
- Validate SQL and read fields back to confirm types
- Ask before running query to populate table with 1 row

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
I'll use **`John_Mike_Customers_Amateur_Chef`** as the name and external key. I checked, and no table with that name exists yet, so it's free. Nothing has been created.

You haven't picked a build option yet, and the name works with either A or B, so I need that before I start. Unless you say otherwise, I'll go with **Option B**, which I recommended. Here's what it creates:

1. **A new table, `John_Mike_Customers_Amateur_Chef`:**
   - It goes in folder 49911, next to `John_Mike_Customers`, and won't be sendable.
   - It gets the same 5 fields as the original: ContactKey (primary key), FirstName, Email, CreatedDate and Bio.
   - After creating it, I'll read the fields back to check that each type came out right.
2. **A SQL Query Activity named `John_Mike_Customers_Amateur_Chef_Query`:**
   - Query: `SELECT ContactKey, FirstName, Email, CreatedDate, Bio FROM John_Mike_Customers WHERE Bio = 'Amateur chef'`
   - It overwrites the new table each time it runs.
   - I'll validate the SQL before saving it.
3. **No run yet.** Once both are built, I'll ask before running the query. When it runs, it should fill the table with 1 row (JMC-0005, Lucas). I'll read the table back afterwards to con

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
