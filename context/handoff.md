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
**Status:** waiting — Filtered table creation blocked by API limits; awaiting user decision on manual creation vs. deletion of standard table.

**Done this session**
- Confirmed native FilteredDataExtension type cannot be created via API
- Identified workaround: manual creation in Email Studio (~2 minutes)
- Documented exact steps for user to create filtered table themselves

**Open items**
- User decision: will you create filtered table manually in Email Studio?
- User decision: keep or delete standard table John_Mike_Customers_Amateur_Chef?
- If keeping standard table: rename it to avoid conflict with filtered table name
- If user creates filtered table: verify it is FilteredDataExtension type and contains JMC-0005
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- Consider scheduling query automation for John_Mike_Customers_Amateur_Chef refresh

**Decisions**
- Option B selected: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100) in new table; all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Query external key truncated by Marketing Cloud to John_Mike_Customers_Amateur_Chef_Que
- Native FilteredDataExtension creation not available via API; manual Email Studio creation required

**Blockers**
- API does not support creating FilteredDataExtension type; only standard Data Extensions can be created programmatically

**Next**
- User confirms: create filtered table manually in Email Studio or proceed with standard table?
- User confirms: delete standard table John_Mike_Customers_Amateur_Chef to free the name, or rename it?
- Once user decides, proceed with TEST-CONTACT-001 phone update and MCP_Email_Send_Test creation

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
You're right. `John_Mike_Customers_Amateur_Chef` is a **standard** table filled by a SQL query, not a native Filtered Data Extension. I built it that way as Option B. It holds the right row, but it isn't the type you asked for. I haven't changed anything this turn.

**What I checked (read-only)**
- **How a native filtered table is built:** I looked at an existing one in the org, `Contacts_With_Gmail_Domain_Email_Id`. It's stored as type **`FilteredDataExtension`**. It's tied to a hidden filter definition, a Filter Activity (type 303) and a link back to its source table.
- **Whether I can create that type:** I can't, with the tools I have. The Data Extension create call takes no filter or source-table settings, so it can only make standard tables. The filtered-table route I tried returned 404. The other route I considered, a filter definition plus a Filter Activity, fills a table, but that table is still standard type. That's the same result you have now, just with a filter instead of SQL.

That's a gap in what I can do here. Email Studio creates these tables itself; I just don't have a way to make one.

**Making it yourself in Email Studio (about 2 minutes)**
1. Go to **Email Studi

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
