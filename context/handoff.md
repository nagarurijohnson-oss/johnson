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
**Status:** on track — John_Mike_Customers DE created & verified in Marketing Cloud. Phone update still blocked (9 sessions).

**Done this session**
- Created John_Mike_Customers data extension in folder 49911 with 4 fields
- Verified all field types saved correctly (ContactKey Text PK, FirstName Text, Email EmailAddress, CreatedDate Date)
- Confirmed DE is empty (0 rows) and ready for data

**Open items**
- User manually edits TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- Load sample rows into John_Mike_Customers DE, or make it sendable if user plans to email contacts
- Escalate persistent confirmation dialog issue to Orchestrate admin — blocking for 9 sessions, requires platform fix

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID PK, Name, Email, Date), not sendable
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 4 fields (ContactKey PK, FirstName, Email, CreatedDate), not sendable unless user specifies

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks IRREVERSIBLE modal display, preventing phone number update write (ninth consecutive session)

**Next**
- Load sample rows into John_Mike_Customers DE, or make it sendable if user plans to email contacts
- Unblock phone update: user manually edits in Contact Builder OR admin enables confirmation dialog in Orchestrate settings
- Escalate confirmation dialog issue to Orchestrate admin for platform fix

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `4a65901d-f270-45ec-96fa-260777323520` |
**In its own words (excerpt):**
I created `John_Mike_Customers` in Marketing Cloud and read it back to check. All four fields saved with the right types.

**Fields (as read back from Marketing Cloud)**

| # | Field | Type | Length | Primary key | Required |
|---|---|---|---|---|---|
| 1 | ContactKey | Text | 50 | Yes | Yes |
| 2 | FirstName | Text | 50 | No | No |
| 3 | Email | EmailAddress | 254 | No | No |
| 4 | CreatedDate | **Date** | — | No | No |

CreatedDate came back as a real Date and Email as EmailAddress, so neither was turned into Text.

**Settings**
- **Folder:** John Orchestrate Test (ID 49911)
- **External key:** `John_Mike_Customers`
- **Sendable:** no
- **Description:** saved as planned
- **Rows:** 0. It's empty and ready for data.

**Finding it:** it's owned by the Orchestrate app user, so your default view in Contact Builder may hide it. Open **Contact Builder → Data Extensions → John Orchestrate Test**, or use [this direct link](https://mc.s13.exacttarget.com/cloud/#app/Contact%20Builder/contactsmeta/admin.html#admin/data-extension/4cac233d-86c1-f111-a5e6-5cba2c19e778/properties/).

**Still open from earlier sessions:** the phone number change for TEST-CONTACT-001 on `John_N_Orchestrate_Test` 

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
