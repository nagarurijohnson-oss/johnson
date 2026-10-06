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
**Status:** blocked — Phone update blocked by confirmation dialog (8th session). User must manually edit or admin must enable dialog.

**Done this session**
- Verified TEST-CONTACT-001 current state in Salesforce org — phone still 12758759879
- Confirmed ContactKey is the data extension key, not Name
- Attempted upsert on John_N_Orchestrate_Test — held by confirmation gate

**Open items**
- Admin enables confirmation dialog in Orchestrate settings, OR user manually edits phone in Contact Builder (TEST-CONTACT-001 12758759879→12758750001, TEST-CONTACT-002 12758759889→12758750002, TEST-CONTACT-003 12758759332→12758750003)
- Execute phone number update via sfmc_bulk_upsert_data_extension_rows on TEST-CONTACT-001, 002, 003
- Read all 5 rows back and verify 3 new numbers saved, 2 unchanged
- User approves creation of Orchestrate_Random_DE DE with 4 fields (ID, Name, Email, Date)
- Create Orchestrate_Random_DE in folder 49911, read back to verify schema and 0 rows

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID primary key, Name, Email, Date), not sendable, no Subscriber Key link
- Proposed update: TEST-CONTACT-001 12758759879→12758750001, TEST-CONTACT-002 12758759889→12758750002, TEST-CONTACT-003 12758759332→12758750003

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks IRREVERSIBLE modal display, preventing phone number update write (eighth consecutive session)

**Next**
- User manually edits TEST-CONTACT-001 phone to 12758750001 in Contact Builder (fastest path), OR admin enables confirmation dialog in Orchestrate settings
- Once unblocked: start new Build session, execute upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- Escalate persistent confirmation dialog issue to Orchestrate admin — blocking for 8 sessions, requires platform fix

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `fc66aba5-e1b4-4913-90ac-03ded943e7e5` |
**In its own words (excerpt):**
I didn't update the phone number. Nothing was written to `John_N_Orchestrate_Test`.

**What I checked (live, just now):**
- `ContactKey` is the data extension's key; `Name` is not. So I searched for `Name = 'John Smith'` first. Exactly **one row** matches out of the 5 in the data extension:

| Field | Now | After the upsert |
|---|---|---|
| ContactKey | TEST-CONTACT-001 | unchanged (the key the upsert matches on) |
| Name | John Smith | unchanged |
| Email | john.smith@example.com | unchanged |
| **Phone** | **12758759879** | **12758750001** |

**What happened:** I sent the upsert with only the Phone value. The tool held it back because it needs you to click **Confirm** in an IRREVERSIBLE confirmation dialog first. The tool that shows that dialog isn't available to me in this session, so I can't show it to you. A "yes" in chat doesn't replace that click, and I won't skip the gate myself. This is the same block that has stopped this exact update in previous sessions. It's a gap on our side, not a Marketing Cloud limitation.

**Two ways to get it done:**
1. **Edit it yourself (quickest):** in Marketing Cloud, go to Contact Builder → Data Extensions → `John_N_Orchestrate_Test` → Reco

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
