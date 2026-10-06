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
**Status:** at risk — Table deleted; orphaned query & filtered table creation remain. Session checked live but cannot create FilteredDataExtension via API.

**Done this session**
- Verified John_Mike_Customers_Amateur_Chef table deletion persists (name free, source table intact)

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
- No API endpoint available to create FilteredDataExtension; Email Studio manual creation required

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
I can't create a native Filtered Data Extension with the tools in this session, so nothing has been created. Email Studio can make one; I can't. That gap is in my tools, not a limit of Marketing Cloud.

**What I checked just now (read-only)**
- **No filtered table exists yet.** Searching for `John_Mike_Customers` finds only the source table, with 5 rows in folder 49911. The name `John_Mike_Customers_Amateur_Chef` is still free, since I deleted my standard table last turn.
- **I tried another route, and it doesn't exist.** `/email/v1/filters/filterdefinition` returned **404 Not Found**. Earlier, `/email/v1/filteredCustomObjects` also returned 404, and the Data Extension create call has no filter or source-table settings. Any table I create comes out as standard type, which is what you said you don't want.

**Create it in Email Studio (about 2 minutes)**
1. Go to **Email Studio → Subscribers → Data Extensions** and open `John_Mike_Customers`.
2. Click **Filter**. Or use **Create → Filtered Data Extension** and pick `John_Mike_Customers` as the source.
3. Drag **Bio** into the filter area and set it to **is equal to** `Amateur chef`.
4. Save it as `John_Mike_Customers_Amateur_Chef` in

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
