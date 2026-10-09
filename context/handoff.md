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
**Status:** at risk — John_Mike_JB_Test fails validation: Bio_Check has wrong operator name and missing field mapping in entry source.

**Done this session**
- Identified two validation errors in Bio_Check: IsNotEmpty operator not recognized, Bio field not in entry source schema
- Confirmed entry source, Send Welcome Email, and data extension are error-free
- Verified journey remains Draft, unmodified, nothing sent

**Open items**
- Fix Bio_Check condition: replace IsNotEmpty operator with correct Marketing Cloud operator name
- Re-select John_Mike_Bio_Split_Test in entry source to load Bio field into journey schema
- Run Validate in Journey Builder after fixes to confirm all errors resolved
- Replace four test email addresses (*.sample@example.com) with controlled addresses before publication
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

**Blockers**
- Bio_Check validation errors prevent publication: wrong operator enum and missing field in entry source schema

**Next**
- Open John_Mike_JB_Test in Journey Builder editor
- Re-select John_Mike_Bio_Split_Test in entry source to load all fields including Bio
- Rebuild Bio_Check condition with correct operator (not IsNotEmpty) and correct comparison operator
- Run Validate in Journey Builder to confirm errors resolved
- Replace test email addresses with controlled ones
- Test journey with entry source automation run

**Checked live on 2026-10-09:** the Salesforce org
### Last session — 2026-10-09
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `01fb15ac-1085-4a83-a04a-d398ce9717b9` |
**In its own words (excerpt):**
**John_Mike_JB_Test fails validation.** Marketing Cloud's validator found errors in **Bio_Check**. The journey can't be published until they're fixed. I didn't change anything, and I checked afterwards that the journey is still **Draft**: never published, last modified 2026-10-09 05:59, the same time as before. Nothing was sent.

This also corrects my last update. I said Bio_Check was "in place", but at that point I had only read it back, not validated it. It saved, but it isn't valid.

**Validation errors** (all in Bio_Check):

| # | Error from Marketing Cloud | What it means |
|---|---|---|
| 1 | `CantConvertDataType`: "The node named 'Condition.Operator' with value 'IsNotEmpty' could not be converted to data type 'OperatorEnum'." | I used the wrong operator name for "Bio is not empty". Marketing Cloud doesn't recognise `IsNotEmpty`. |
| 2 | `121408` (reported twice, once for each Bio condition): "Path HasBio has criteria which uses a field "Bio" that does not exists in the Journeys entry event schema." | The data extension does have Bio. But the entry source I created has no field list, so the journey can't see Bio. |

**What passed:**
- **Entry source:** no errors. `DEAudience-

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
