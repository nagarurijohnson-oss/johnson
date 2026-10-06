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
**Status:** at risk — Phone update still blocked by confirmation dialog (9 sessions). New DE schema ready for approval.

**Done this session**
- Verified John_Mike_Customers name is available in Marketing Cloud
- Designed John_Mike_Customers schema: ContactKey (PK), FirstName, Email, CreatedDate

**Open items**
- User manually edits TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- User approves John_Mike_Customers schema (ContactKey PK, FirstName, Email, CreatedDate) and folder 49911
- Create John_Mike_Customers DE in folder 49911, read back to verify schema and 0 rows

**Decisions**
- John_N_Orchestrate_Test: Standard DE, folder 32375, upsert method, confirmation gate required
- Orchestrate_Random_DE: Standard DE, folder 49911, external key John_Mike, 4 fields (ID primary key, Name, Email, Date), not sendable
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 4 fields (ContactKey PK, FirstName, Email, CreatedDate), not sendable unless user specifies

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks IRREVERSIBLE modal display, preventing phone number update write (ninth consecutive session)

**Next**
- User approves John_Mike_Customers schema or requests changes (folder, sendable flag, field nullability)
- Once approved: create John_Mike_Customers, read back schema to verify all field types saved correctly
- Unblock phone update: user manually edits in Contact Builder OR admin enables confirmation dialog in Orchestrate settings
- Escalate persistent confirmation dialog issue to Orchestrate admin — blocking for 9 sessions, requires platform fix

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `4a65901d-f270-45ec-96fa-260777323520` |
**In its own words (excerpt):**
I checked Marketing Cloud first, and there's no existing data extension that matches "John_Mike", so the name is free. I haven't created anything yet. Here's what I'll build once you confirm.

**Data extension to create: `John_Mike_Customers`**

| # | Field | Type | Length | Primary key | Required |
|---|---|---|---|---|---|
| 1 | ContactKey | Text | 50 | Yes | Yes |
| 2 | FirstName | Text | 50 | No | No |
| 3 | Email | EmailAddress | 254 | No | No |
| 4 | CreatedDate | Date | — | No | No |

**Settings I'll use unless you change them:**
- **Folder:** "John Orchestrate Test" (ID 49911, under Data Extensions). It exists in the account, and your earlier sessions used it for new data extensions.
- **External key:** `John_Mike_Customers`, the same as the name.
- **Sendable:** no. If you plan to send email to it, I can make it sendable instead, with ContactKey linked to Subscriber Key.
- **Description:** "Customer list with contact key, first name, email and created date."

**How I'll do it:**
1. Create the data extension with the field list above.
2. Read the fields back and check that every type actually saved. Marketing Cloud can quietly turn an unrecognised type into Text, so I'll sp

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
