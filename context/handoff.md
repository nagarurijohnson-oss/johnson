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
**Status:** on track — Query table populated & verified (1 row). Ready for MCP_Email_Send_Test template selection & contact update.

**Done this session**
- Confirmed John_Mike_Customers_Amateur_Chef populated with 1 row (Lucas, JMC-0005)
- Verified all field values match source table
- Confirmed source table unchanged

**Open items**
- Pick template (A or B) for MCP_Email_Send_Test creation
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Consider scheduling query automation for John_Mike_Customers_Amateur_Chef refresh
- Consider widening Bio field if bios >100 chars may be added to source

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100) in new table; all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Query external key truncated by Marketing Cloud to John_Mike_Customers_Amateur_Chef_Que

**Blockers**
- None

**Next**
- Select template A or B for MCP_Email_Send_Test
- Update TEST-CONTACT-001 phone number to 12758750001
- Create MCP_Email_Send_Test in folder 49889

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
The query has run, and `John_Mike_Customers_Amateur_Chef` now has the filtered record. I read the table back and it has **1 row**:

| ContactKey | FirstName | Email | CreatedDate | Bio |
|---|---|---|---|---|
| JMC-0005 | Lucas | lucas.sample@example.com | 10/6/2026 9:48:31 AM | Amateur chef |

- **It matches the source.** This is the only row in `John_Mike_Customers` where Bio = 'Amateur chef', and every value is the same as in that table. The CreatedDate is the original value carried over, not the time the query ran.
- **The source table didn't change.** `John_Mike_Customers` still has its 5 rows.

**Things to know:**
- **It won't update on its own.** This is a table filled by a SQL query, not a native filtered table, so it only changes when the query runs. If you add more "Amateur chef" rows to `John_Mike_Customers`, they won't appear here until the query runs again. I can put the query in a scheduled automation so it refreshes on its own.
- **Bio only holds 100 characters** in the new table, while the source field has no limit. If a matching bio is ever longer than 100 characters, the query will fail. I can widen the field if you want to cover that.

**Still open from earlier s

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
