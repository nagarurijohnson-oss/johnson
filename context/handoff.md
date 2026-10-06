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
**Status:** blocked — 5 sample rows ready but blocked by confirmation dialog — user must import CSV manually or admin enables dialog

**Done this session**
- Verified John_Mike_Customers still empty (0 rows)
- Prepared 5 sample rows CSV with all fields and bios ≤20 chars

**Open items**
- User imports John_Mike_Customers_sample_rows.csv manually via Contact Builder, or admin enables confirmation dialog
- Read back all 5 rows from John_Mike_Customers to verify import succeeded
- User confirms template choice (A or B) for MCP_Email_Send_Test creation
- Create MCP_Email_Send_Test in folder 49889 with external key MCP_Email_Send_Test
- User manually updates TEST-CONTACT-001 phone to 12758750001 in Contact Builder, OR admin enables confirmation dialog
- Execute phone number update via upsert on John_N_Orchestrate_Test, read back all 5 rows to verify
- Escalate persistent confirmation dialog issue to Orchestrate admin (blocking 10+ sessions)

**Decisions**
- Bio field: Text type, length 20 chars, optional, added to John_Mike_Customers
- Sample rows: 5 test contacts (JMC-0001 to JMC-0005) with realistic names, test emails, and short bios
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- MCP_Email_Send_Test: will be created in folder 49889 with external key MCP_Email_Send_Test — awaiting template selection

**Blockers**
- Confirmation dialog unavailable — platform/admin setting blocks irreversible modal display (tenth+ session)
- Template choice (A or B) required before MCP_Email_Send_Test creation can proceed

**Next**
- User imports CSV via Contact Builder → Data Extensions → John_Mike_Customers → Import, or admin enables dialog
- Read back all 5 rows to confirm import succeeded
- User provides template choice (A or B) for MCP_Email_Send_Test
- Escalate confirmation dialog blocker to Orchestrate admin

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `4a65901d-f270-45ec-96fa-260777323520` |
**In its own words (excerpt):**
The 5 rows are not in `John_Mike_Customers` yet. Nothing was written, and the data extension still has 0 rows.

**Why it stopped:** Orchestrate treats a data extension row write as irreversible. Before it will run the insert, you have to click Confirm on an acknowledgement dialog, and I can't open that dialog in this session. It's the same blocker that has held up the TEST-CONTACT-001 phone change. I also didn't push the rows through a different write tool, because that would skip the check you're meant to approve.

**Import them yourself in about a minute.** I've attached a CSV with the 5 rows exactly as listed to this session.
1. Open **Contact Builder → Data Extensions → John Orchestrate Test → John_Mike_Customers**.
2. Click **Import**, choose the attached `John_Mike_Customers_sample_rows.csv`, and set the delimiter to comma.
3. Choose **Add and Update**. Check that the 5 columns map to the matching fields; the names are identical. The dates are in YYYY-MM-DD format.
4. Finish the import. Then tell me, and I'll read the rows back and confirm all 5 landed correctly.

**Or get the dialog fixed:** an Orchestrate admin can turn the confirmation dialog back on. After that, I can ins

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
