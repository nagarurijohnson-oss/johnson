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
**Status:** on track — Bio_Check validation fixed. Journey ready for manual test in Journey Builder; no API test available.

**Done this session**
- Confirmed journey test capability exists in Journey Builder UI (no API endpoint found)
- Verified test can run without publishing or sending email to sample addresses
- Documented expected test routing: JMC-0001, JMC-0002 → Has Bio; JMC-0003, JMC-0005 → Remainder

**Open items**
- Run manual test in Journey Builder (select contacts, validate, test, leave send email off)
- Replace four *.sample@example.com test addresses with controlled addresses before publishing
- Publish John_Mike_JB_Test journey after test confirms routing
- Run entry source automation to test actual contact routing through journey
- Resolve testOrchestrateMap error from previous automation run

**Decisions**
- Entry source: DEAudience-John_Mike_JB_Test-20261009 from John_Mike_Bio_Split_Test, no schedule
- Bio_Check condition 1: IsNotNull operator
- Bio_Check condition 2: NotEqual 'No Biography is Available here.'
- Test method: manual in Journey Builder UI (no API available)
- Test email sending: leave unticked to avoid delivery to sample addresses

**Blockers**
- None

**Next**
- Open John_Mike_JB_Test in Journey Builder and run manual test with 4 test contacts
- Verify routing matches expected paths (Has Bio vs Remainder)
- Replace sample email addresses with controlled addresses
- Publish journey and monitor real contact routing

**Checked live on 2026-10-09:** the Salesforce org, the web
### Last session — 2026-10-09
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `01fb15ac-1085-4a83-a04a-d398ce9717b9` |
**In its own words (excerpt):**
**Yes. You can test `Bio_Check` without publishing the journey or sending email, but only from the Journey Builder screen.** I couldn't find a way to run the test through the API, so I can't run it for you. I didn't change or run anything: John_Mike_JB_Test is still **Draft**, nobody has entered it, and it was last modified at 06:33:50, the time of the last fix.

**Why it qualifies** (checked on the journey today):

| What Test needs | John_Mike_JB_Test |
|---|---|
| A Data Extension entry source | Yes: `DEAudience-John_Mike_JB_Test-20261009`, reading from `John_Mike_Bio_Split_Test` |
| The journey must pass validation first, which is what turns on the **Test** button | Yes: 0 errors and 0 warnings in the last validation |
| The journey must still be a draft | Yes: never published, and nobody has entered it |
| The split must use the entry data's fields | Yes: Bio_Check reads `Event.DEAudience-John_Mike_JB_Test-20261009.Bio` |

**How the test works:**
- You pick one or more test contacts from the 4 rows in `John_Mike_Bio_Split_Test`. The test runs each one through the journey without publishing it.
- Decision Splits are worked out from the real data, so Bio_Check routes each contac

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
