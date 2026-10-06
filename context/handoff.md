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
**Status:** at risk — Query deletion awaiting explicit confirmation; filtered table creation still pending user action in Email Studio.

**Done this session**
- None

**Open items**
- User confirms 'Confirm delete query' to remove orphaned John_Mike_Customers_Amateur_Chef_Query (ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
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
- Query deletion requires explicit user confirmation before proceeding

**Next**
- User replies 'Confirm delete query' to authorize deletion of John_Mike_Customers_Amateur_Chef_Query
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
I haven't deleted anything yet. The safety check stopped the delete because deleting the query is permanent, and it wants an explicit confirmation for this specific action. This session can't show the on-screen Confirm pop-up. Your "proceed" didn't name what to delete, so I'd rather ask once than assume.

**What would be deleted**
- **Query:** SQL Query Activity `John_Mike_Customers_Amateur_Chef_Query`, ID `6aeb4e3d-2568-4f50-9acb-f469a7cce4c6`, in the root Query folder (32395) in Automation Studio. That's 1 query.
- **What it does:** it copies rows from `John_Mike_Customers` where Bio = 'Amateur chef' into a table called `John_Mike_Customers_Amateur_Chef`, replacing that table's contents each run. That table was deleted last turn.
- **Automations:** none of the 27 automations I looked at appear to use this query, and I never added it to one. That's based on their names and descriptions; I didn't open each one's steps.
- **What stays:** `John_Mike_Customers` and its 5 rows aren't affected. You lose no data, because the query only copies rows.

**What I'll do once you confirm**
1. Delete query `6aeb4e3d-2568-4f50-9acb-f469a7cce4c6`.
2. Look it up again to confirm it's gone.

Reply *

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
