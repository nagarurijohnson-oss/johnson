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
**Status:** waiting — Located John_Mike_Customers_Amateur_Chef table; awaiting user confirmation to delete table ± query

**Done this session**
- Located John_Mike_Customers_Amateur_Chef table (ID d67281f5-9fc1-f111-a5e6-5cba2c19e778) in folder 49911
- Confirmed table contains 1 row (JMC-0005) and original data safe in John_Mike_Customers
- Identified orphaned query John_Mike_Customers_Amateur_Chef_Query that writes to table

**Open items**
- User confirms: delete table only (a) or delete table + query (b)?
- If user confirms deletion: execute delete and verify name is freed
- Create filtered table manually in Email Studio (FilteredDataExtension type)
- Verify filtered table contains JMC-0005
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Consider scheduling query automation for John_Mike_Customers refresh

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100) in new table; all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Query external key truncated by Marketing Cloud to John_Mike_Customers_Amateur_Chef_Que
- Native FilteredDataExtension creation not available via API; manual Email Studio creation required

**Blockers**
- Awaiting user confirmation before permanent deletion of table and query

**Next**
- User replies with 'Confirm (a)', 'Confirm (b)', or 'Cancel'
- If confirmed: delete table ± query and verify name is freed
- User creates filtered table in Email Studio under name John_Mike_Customers_Amateur_Chef

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
I found the table and haven't deleted anything yet. Deleting can't be undone, so I need your confirmation first.

**What would be deleted**
- **Table:** `John_Mike_Customers_Amateur_Chef`. It's the standard table I built earlier, with external key `John_Mike_Customers_Amateur_Chef`, ID `d67281f5-9fc1-f111-a5e6-5cba2c19e778`, in folder 49911.
- **Its contents:** 5 fields and **1 row** (JMC-0005, Lucas, lucas.sample@example.com, Amateur chef). That row is a copy, and the original is still in `John_Mike_Customers`, so you don't lose any data.
- **What stays:** `John_Mike_Customers` and its 5 rows aren't touched.

**One decision before I delete:** the SQL query `John_Mike_Customers_Amateur_Chef_Query` writes into this table. Once the table is gone, the query has nowhere to write, and it will fail if anyone runs it. Your choices:
- **(a) Delete the table only.** The query stays as it is.
- **(b) Delete the table and the query.** I'd recommend this, since the query has no use without the table. It's also permanent.

**What I'll do once you confirm**
1. **Delete the table:** delete Data Extension `d67281f5-9fc1-f111-a5e6-5cba2c19e778`.
2. **Delete the query (option b only):** delete Query

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
