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
**Status:** at risk — AUTO_Daily_Data_Load created but two blockers remain: wrong run time (7 AM not 9 AM IST) and target table missing

**Done this session**
- Confirmed AUTO_Daily_Data_Load exists and is Scheduled in folder 32393
- Verified step John_Mike_Customers_Amateur_Chef_Query is attached
- Identified target table deletion: query writes to ___John_Mike_Customers_Amateur_Chef_1
- Provided navigation path to automation in Automation Studio

**Open items**
- Fix automation run time: user to open Schedule UI, set 9:00 AM India Standard Time, click Done and Save
- Recreate target table John_Mike_Customers_Amateur_Chef (5 fields: ContactKey PK, FirstName, Email, CreatedDate, Bio)
- Verify query points to recreated table after restoration
- Read back automation schedule after time correction to confirm 9:00 AM IST is stored
- User creates filtered table JNOT_CreatedDate_0938_Filtered in Email Studio UI
- Verify filtered table type, source, and row count (expect 10: TEST-CONTACT-006 to 015)
- Clarify: restore JMC-0004 FirstName from 'Updated' to 'Meera' or leave as-is
- Execute two-step method on JMC_Amateur_Chef_Filtered

**Decisions**
- Step for AUTO_Daily_Data_Load: John_Mike_Customers_Amateur_Chef_Query (SQL Query Activity, ID 6aeb4e3d-2568-4f50-9acb-f469a7cce4c6)
- Automation folder: 32393, time zone: India Standard Time, recurrence: daily
- Option B: Standard table + SQL Query Activity for John_Mike_Customers_Amateur_Chef
- Bio field: Text(100); all current bios fit
- John_Mike_Customers: Standard DE, folder 49911, external key John_Mike_Customers, 5 fields, not sendable
- Filter condition: within-the-minute (CreatedDate = 10/6/2026 9:38:48 AM) for 10 rows

**Blockers**
- Target table John_Mike_Customers_Amateur_Chef missing — automation will fail on each run until recreated
- Schedule stored as 2026-10-07T19:30 CST (8 Oct 7:00 AM IST) instead of 9:00 AM IST — user must correct in UI

**Next**
- User opens AUTO_Daily_Data_Load in Automation Studio (folder 32393), clicks Schedule, sets 9:00 AM India Standard Time, saves
- User confirms: recreate target table John_Mike_Customers_Amateur_Chef with 5 fields and ContactKey as primary key
- Verify query John_Mike_Customers_Amateur_Chef_Query points to recreated table
- Read back automation schedule to confirm 9:00 AM IST is now stored correctly

**Checked live on 2026-10-06:** the Salesforce org
### Last session — 2026-10-06
| | |
|---|---|
| Type | BUILD |
| Outcome | COMPLETED |
| Branch | `orchestrate/context` |
| Session | `58b3d8ba-c450-493f-9233-a0d9e3d2720f` |
**In its own words (excerpt):**
I can't give you a direct link to `AUTO_Daily_Data_Load`. Marketing Cloud web links include your account's server stack (for example `mc.s11.exacttarget.com`), and nothing I can read from here tells me which stack yours is on. I'd rather not guess a URL that might not open.

This gets you there:

1. Log in at **https://mc.exacttarget.com**. It sends you to your own stack automatically.
2. Go to **Journey Builder → Automation Studio**.
3. Open folder **32393** and click **`AUTO_Daily_Data_Load`**. You can also search for that name.

Once it's open, you can copy the address from your browser to keep as a direct link.

I just checked it again (ID `21f21dab-f5f1-4ef9-950c-21ebd13e7cbb`). Both problems from last time are still there:
- **Run time:** the stored start is `2026-10-07T19:30` server time, which is 8 Oct at 7:00 AM IST, not 9:00 AM. While you have it open, click **Schedule**, set **9:00 AM, India Standard Time**, then **Done** and **Save**.
- **Target table:** the query still writes to `___John_Mike_Customers_Amateur_Chef_1`. That name usually means the original table was deleted. Reply **"recreate the table"** and I'll rebuild `John_Mike_Customers_Amateur_Chef`.

If you mean

_[summary truncated — see the session record for the full text]_
<!-- orchestrate:session-state:end -->
