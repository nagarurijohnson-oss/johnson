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
### Engagement state — 2026-10-09
**Status:** at risk — Bio_Check operator identified as IsNotNull; entry source Bio exposure unconfirmed. Fix ready for approval.

**Done this session**
- Identified correct operator: IsNotNull (not IsNotEmpty) — confirmed in 10 uses across 6 journeys
- Analyzed Bio field exposure: entry source points to correct DE but field list cannot be verified via API
- Identified likely root cause: Bio field wrapped in quotes and missing IsEphemeralAttribute marker in XML
- Proposed exact fix: rewrite both Bio_Check conditions in editor format with IsNotNull operator

**Open items**
- Get approval for proposed Bio_Check rewrite before applying changes
- Apply fix: change IsNotEmpty to IsNotNull and align XML format (remove quotes, add IsEphemeralAttribute)
- Run Validate in Journey Builder to confirm operator and Bio field errors resolved
- If Bio error persists after fix, update entry source field exposure
- Replace four test email addresses (*.sample@example.com) with controlled addresses
- Run entry source automation or journey to test actual routing of four test rows
- Resolve error message from testOrchestrateMap activity in previous session automation run

**Decisions**
- Entry source: DEAudience-John_Mike_JB_Test-20261009 from John_Mike_Bio_Split_Test, no schedule
- Bio_Check condition: Bio is not empty AND Bio is not 'No Biography is Available here.'
- Recipient email: entry data Email field (not contact default)
- Journey path: Entry source → Send Welcome Email → Bio_Check (Has Bio / Remainder) → End
- Error notification: nagaruri.johnson@jaxconsult.com
- Cutoff filter: CreatedDate >= '2026-10-06 09:38:49'
- Fix approach: use Journey Builder editor (more reliable than API)
- Operator for 'is not empty': IsNotNull (confirmed in 10 uses, 6 journeys)

**Blockers**
- Bio_Check validation errors prevent publication: IsNotEmpty operator not recognized; Bio field not matched in entry source schema

**Next**
- Present exact XML changes for Bio_Check conditions to stakeholder for approval
- Upon approval: open John_Mike_JB_Test in Journey Builder editor
- Rewrite both Bio_Check conditions: change IsNotEmpty to IsNotNull, remove quotes around Bio, add IsEphemeralAttribute=true
- Run Validate in Journey Builder to confirm errors resolved
- If Bio error persists, investigate entry source field exposure and update if needed

**Checked live on 2026-10-09:** the Salesforce org, the web
### Last session — 2026-10-09
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `01fb15ac-1085-4a83-a04a-d398ce9717b9` |
**In its own words (excerpt):**
The operator for "Bio is not empty" is **`IsNotNull`**. I can't confirm the entry source exposes `Bio`, because Marketing Cloud's API doesn't return a field list for this type of entry source. I didn't change anything, and John_Mike_JB_Test is still **Draft**.

**1. Supported operators**

I couldn't get the full official list. Salesforce's operator reference page blocked access (HTTP 403), and the search results didn't give exact names. So the list below is only what I could check in your tenant's 20 journeys:

| Operator | Used in your splits | Status |
|---|---|---|
| `IsNotNull` | 10 times, in 6 journeys | This is "is not empty". |
| `Equal` | 3 times | Used in your journeys. |
| `NotEqual` | Once, in Bio_Check | Didn't cause a validation error, so it's fine for "Bio is not the default text". |
| `IsNotEmpty` | Once, in Bio_Check only | **Not valid.** The validator rejected it (`CantConvertDataType`). |

The strongest evidence is the **"DE entry source"** journey (created 2026-10-08). It was built in the editor and splits on a field also called `Bio`:

```
<Condition IsEphemeralAttribute="true" Key="Event.DEAudience-5c2339f6-….Bio" Operator="IsNotNull" UiMetaData="{}"><Value><![

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
