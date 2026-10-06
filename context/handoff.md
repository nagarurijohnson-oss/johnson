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
**Status:** at risk — API filtered table creation attempted; awaiting user confirmation on query deletion approach (a) or (b)

**Done this session**
- Verified John_Mike_Customers has 5 rows; JMC-0005 (Lucas) matches Bio = 'Amateur chef'
- Confirmed no filtered table exists yet
- Located working FilteredDataExtension example (Filtered_DE_Test_Ashwin) to model format
- Identified old query still present; will overwrite if filtered table uses same name

**Open items**
- User confirms approach (a) delete query or (b) rename filtered table to avoid overwrite
- Create saved filter on John_Mike_Customers (Bio equals 'Amateur chef') via API
- Create filtered table John_Mike_Customers_Amateur_Chef via API (uncertain endpoint)
- If API creation fails: user creates filtered table manually in Email Studio
- Verify filtered table type is FilteredDataExtension and contains JMC-0005
- If (a) chosen: obtain explicit delete confirmation for query 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100) in new table; all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Query external key truncated by Marketing Cloud to John_Mike_Customers_Amateur_Chef_Que
- Attempt API creation of FilteredDataExtension before falling back to Email Studio manual creation

**Blockers**
- Old query John_Mike_Customers_Amateur_Chef_Query will overwrite filtered table if both use same name
- FilteredDataExtension creation endpoint uncertain; may require Email Studio fallback

**Next**
- User replies 'Proceed with (a)' or 'Proceed with (b)' to resolve query/table name conflict
- Attempt API creation of saved filter and filtered table; report exact errors if rejected
- If API fails: provide Email Studio manual creation steps (Subscribers → Data Extensions → John_Mike_Customers → Filter → Bio equals 'Amateur chef')

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I haven't created anything yet; I need your go-ahead first. Last session concluded this had to be done by hand in Email Studio, but I've now found an API path to try first.

**What I checked (read-only)**
- `John_Mike_Customers` has 5 rows. One matches Bio = 'Amateur chef': **JMC-0005 (Lucas)**.
- No filtered table from it exists yet.
- A working filtered table in your account (`Filtered_DE_Test_Ashwin`) shows how one is built: a table of type `FilteredDataExtension` linked to its source table and a saved filter. The filter endpoint for that example responds and returns the full filter definition, so I can copy its format exactly.
- The old query `John_Mike_Customers_Amateur_Chef_Query` (ID `6aeb4e3d-…`) is still there. It writes to the old table name, which no longer exists.

**Proposed plan**
1. **Create the filter:** a saved filter on `John_Mike_Customers` with Bio equals "Amateur chef", modelled on the working example.
2. **Create the filtered table:** `John_Mike_Customers_Amateur_Chef` from that filter, in the same folder as the source (49911). This is the uncertain step. No endpoint I've found so far creates the filtered-table record itself. I'll try the likely ones and show 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
