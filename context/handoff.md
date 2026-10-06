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
**Status:** at risk — Table deleted successfully; orphaned query remains and risks interfering with filtered table creation

**Done this session**
- Deleted John_Mike_Customers_Amateur_Chef table (ID d67281f5-9fc1-f111-a5e6-5cba2c19e778) via REST API
- Verified table deletion: lookup by ID returns 'not found', name search shows only John_Mike_Customers
- Confirmed source table John_Mike_Customers intact with 5 rows in folder 49911

**Open items**
- User confirms deletion of orphaned query John_Mike_Customers_Amateur_Chef_Query (reply 'delete the query')
- User creates filtered table John_Mike_Customers_Amateur_Chef in Email Studio (Bio equals 'Amateur chef')
- Verify filtered table is FilteredDataExtension type and contains JMC-0005 (Lucas)
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Consider scheduling query automation for John_Mike_Customers refresh

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100) in new table; all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Query external key truncated by Marketing Cloud to John_Mike_Customers_Amateur_Chef_Que
- Native FilteredDataExtension creation not available via API; manual Email Studio creation required
- Table deletion proceeded via REST API after SOAP attempts failed with Token Expired

**Blockers**
- Orphaned query John_Mike_Customers_Amateur_Chef_Query will fail if run and may overwrite filtered table if recreated under same name

**Next**
- User replies 'delete the query' to remove orphaned query
- User creates filtered table in Email Studio: Subscribers → Data Extensions → John_Mike_Customers → Filter → Bio equals 'Amateur chef' → save as John_Mike_Customers_Amateur_Chef in folder 49911
- Verify filtered table creation and JMC-0005 presence

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
I deleted the table `John_Mike_Customers_Amateur_Chef`, and it's gone from Marketing Cloud. Looking up its ID now returns "not found", and searching for the name only finds `John_Mike_Customers`.

- **Your source table wasn't affected.** `John_Mike_Customers` still has its 5 rows and 5 fields in folder 49911.
- **The name is free.** You can now create the filtered table in Email Studio as `John_Mike_Customers_Amateur_Chef`.
- **How it went through:** I tried deleting through one Marketing Cloud API (SOAP) twice, and both attempts failed with "Token Expired". Nothing was deleted by those attempts. I then deleted it through the other API (REST), which worked. I passed the safety-check flag myself based on your typed "Confirm".

**The query is still there.** You replied "Confirm" without saying (a) or (b). Both options delete the table, so I did that part only. The query `John_Mike_Customers_Amateur_Chef_Query` now points at a table that doesn't exist. If anyone runs it, it will fail. Once you create your filtered table under the same name, the query would overwrite its contents and could interfere with it. I'd recommend deleting the query too. Reply **"delete the query"** if you want

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
