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
**Status:** on track — Journey validated and ready for manual test in Journey Builder UI; sample email addresses still need replacement before publish

**Done this session**
- Confirmed John_Mike_JB_Test passes validation (0 errors, 0 warnings)
- Verified entry source DEAudience-John_Mike_JB_Test-20261009 is correct and linked
- Confirmed Bio_Check split logic routes correctly based on Bio field conditions
- Documented test method: manual in Journey Builder (no API available)

**Open items**
- Run manual test in Journey Builder with 4 test contacts, verify routing matches expected paths
- Replace four *.sample@example.com test addresses with controlled addresses before publishing
- Publish John_Mike_JB_Test journey after test confirms routing
- Run entry source automation to test actual contact routing through journey
- Resolve testOrchestrateMap error from previous automation run

**Decisions**
- Entry source: DEAudience-John_Mike_JB_Test-20261009 from John_Mike_Bio_Split_Test, no schedule
- Bio_Check condition 1: IsNotNull operator
- Bio_Check condition 2: NotEqual 'No Biography is Available here.'
- Test method: manual in Journey Builder UI only (no API endpoint exists)
- Test email sending: leave unticked to avoid delivery to sample addresses

**Blockers**
- None

**Next**
- Open John_Mike_JB_Test in Journey Builder and select Test button
- Run manual test with all 4 contacts from John_Mike_Bio_Split_Test, verify routing (JMC-0001, JMC-0002 → Has Bio; JMC-0003, JMC-0005 → Remainder)
- Replace sample@example.com addresses with controlled test addresses
- Publish journey after test confirms expected routing

**Checked live on 2026-10-09:** the Salesforce org
### Last session — 2026-10-09
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `01fb15ac-1085-4a83-a04a-d398ce9717b9` |
**In its own words (excerpt):**
**John_Mike_JB_Test checks out and passes validation with 0 errors and 0 warnings.** It can be tested without publishing or sending email, but only from the Journey Builder screen, not through the API. One limit on what I checked: I can't open the Journey Builder screen myself. Everything below comes from Marketing Cloud's API.

I didn't modify, publish, activate or run the journey. The only extra call was a fresh validation, which checks the configuration without changing anything. Afterwards the journey was still **Draft**, never published, with 0 contacts entered and last modified at 06:33:50, the time of the last fix.

**Entry source: correct**
- `DEAudience-John_Mike_JB_Test-20261009` is a Data Extension entry source reading from `John_Mike_Bio_Split_Test`.
- It has no schedule. Its backing automation ("DEAudience John_Mike_JB_Test – 2026-10-09T055854.154") also has no schedule, and its status is Ready.
- It's linked to 1 journey, and that journey isn't published.
- The data extension is sendable (ContactKey is linked to Subscriber Key). It has 5 fields, including Bio (Text 4000), and 4 rows.

**Send Welcome Email: correct**
- It uses email 10606 with the subject `Welcome, %%F

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
