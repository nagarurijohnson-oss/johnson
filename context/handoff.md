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
**Status:** waiting — Awaiting user choice (A/B/C) for filtered table build; JMC-0004 updated, 4 open items remain

**Done this session**
- None

**Open items**
- User selects option A, B, or C for filtered table (John_Mike_Customers_Amateur_Chef)
- Pick template (A or B) for MCP_Email_Send_Test creation
- Update TEST-CONTACT-001 phone to 12758750001 in Contact Builder
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test

**Decisions**
- Bio field: Text type, no length limit, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- CreatedDate populates with GetDate() default on import
- Safety check: send update without confirmation flag; if blocked, pass flag based on user's typed confirmation

**Blockers**
- None

**Next**
- User replies with A, B, or C (plus any name/folder changes) for filtered table
- Once chosen: create target table, build filter or query, ask before running
- User selects template for MCP_Email_Send_Test
- User updates TEST-CONTACT-001 phone in Contact Builder

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `main` |
| Session | `f98da8e8-f066-4149-bfcb-7eaca34f39fa` |
**In its own words (excerpt):**
Nothing has been created yet. Before I build, I need you to choose how to do it, because Marketing Cloud's "Filtered Data Extension" can mean more than one thing here.

**What I checked (read-only)**
- `John_Mike_Customers` has exactly **1 row** where Bio = 'Amateur chef': **JMC-0005, Lucas, lucas.sample@example.com**. The new table will start with that one row.
- The filtered table you see in Email Studio is built from a **filter definition** sitting on the source table. I don't have a dedicated tool for that type of table. I can reach the filter-definition object through the general SOAP access, but my API reference doesn't cover the create call. So this route is untested here and may need a few attempts.

**Three ways to do it**

| Option | What gets built | Notes |
|---|---|---|
| **A. Filter definition + Filter Activity** | A filter on `John_Mike_Customers` (Bio equals 'Amateur chef'), a new target table, and a Filter Activity that fills it | Closest to a native filtered table that I can make through the API. Untested in this session, so it may not work on the first try. |
| **B. Standard table + SQL Query** *(my recommendation)* | A new table with the same 5 fields, plus a SQ

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
