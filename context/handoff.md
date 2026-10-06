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
**Status:** on track — Query ready to run; awaiting user confirmation to execute or widen Bio field first

**Done this session**
- Verified John_Mike_Customers_Amateur_Chef table exists, empty, 0 rows
- Verified John_Mike_Customers has 1 matching row (JMC-0005, Lucas)
- Confirmed query John_Mike_Customers_Amateur_Chef_Query is validated and ready

**Open items**
- User confirms: run query now or widen Bio field to unlimited first
- Run query to populate John_Mike_Customers_Amateur_Chef with Lucas row
- Read table back after query run to confirm 1 row populated
- Pick template (A or B) for MCP_Email_Send_Test creation
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100) in new table; source has no limit but all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Query external key truncated by Marketing Cloud to John_Mike_Customers_Amateur_Chef_Que

**Blockers**
- None

**Next**
- User replies: 'run it' or 'widen Bio, then run it'
- Execute query to populate John_Mike_Customers_Amateur_Chef
- Read table back to confirm Lucas row present and field types correct
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
`John_Mike_Customers_Amateur_Chef` is empty because the query that fills it hasn't run yet. Last turn I only created the table and the query, and I stopped to get your OK before running it. A table built this way only gets rows when the SQL Query Activity runs, unlike a native filtered table in Email Studio. Nothing is broken.

I just checked both tables:
- **`John_Mike_Customers_Amateur_Chef`:** 0 rows.
- **`John_Mike_Customers`:** exactly 1 row where Bio = 'Amateur chef', which is **JMC-0005, Lucas, lucas.sample@example.com**. That's the row the query will copy across.

**What I'll do once you confirm**
1. **Run the query** `John_Mike_Customers_Amateur_Chef_Query`. Each run replaces everything in `John_Mike_Customers_Amateur_Chef`, but the table is empty now, so nothing is lost. `John_Mike_Customers` isn't touched.
2. **Check the result.** The query runs in the background, so I'll read `John_Mike_Customers_Amateur_Chef` back and confirm it has 1 row with Lucas's values.

**Optional:** the Bio field in the new table only holds 100 characters, but in the source it has no limit. Lucas's bio is 12 characters, so this run works either way. If you want, I can widen Bio first so a longe

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
