## Day Summary Header

- **Date:** 2026-07-17 (Friday)
- **Notion page:** https://app.notion.com/p/3a07a5e7c4ee810c96b9f359fc63f284
- **Work windows:** 1:00-11:00pm (IST), including lunch and dinner within the span
- **Recurring calls today:** none — confirmed no calls at all on Fridays (Elastic SME call included). `resources/recurring-schedule.md` updated.
- **Schedule shape:** office 1:00-7:30pm, commute 7:30-9:00pm, dinner at home 9:00-9:30pm, then continue working until 11:00pm.
- **Skilling:** placed 6:00-7:00pm (last hour before leaving office).
- **Total estimated task-work:** 5.75h (vs ~6.5h available after lunch/commute/dinner/skilling; ~0.75h buffer)
- **Check-in trigger ids:** trig_01NaN9UiYYmdJVArFqjUDwaT (3:00pm), trig_019KpF7U8VxcWe3wxThoiKZd (5:00pm), trig_01Fmbzw8FmG9GX8B3HkeN3K8 (7:00pm), trig_01PsvxSihWF8HnfQu11R46c7 (9:30pm), trig_012eyz6SY9tHtZtQtu2pR7qj (11:15pm wrap-up) — all IST.
- **Status:** wrapped-up — several items unconfirmed (no reply to 4 consecutive check-ins after 3pm); see Day Summary

## Tasks

| # | Task | Time | Priority/Deadline | Est. (h) | Status | Actual (h) | Check-in Update |
|---|------|------|--------------------|----------|--------|------------|------------------|
| 1 | Follow up with Deepak re: Prisma alerts (not yet received) | 1:00-1:15pm | - | 0.25 | not started | | |
| 2 | Finish Task 2: CMEK validation (missing key-vault role) | 1:15-2:00pm, 2:30-2:45pm | Priority | 1.0 | mostly working — roles added and running; intermittent Vault issue remains, but at 4:30pm was told the Vault team is aware and already working on it (not on the user to fix) | | |
| 3 | Task 3: Raise ≥4 Prisma tickets, Jira, forward to Deepak | 2:45-3:45pm | - | 1.0 | not started | | |
| 3b | (ad hoc) Helped Karthik create components in AITAPC using the IDP tool | ~3:45pm | - | ? | done — duration unconfirmed | | |
| 4 | Phase-2 review (confirm alignment, coordinate w/ Timothy McDonald) | 3:45-4:15pm | - | 0.5 | not started | | |
| 5 | Elastic follow-up: verify Sudhir's deployment via testing, update status emails | 4:15-5:15pm | - | 1.0 | not started | | |
| 6 | Kalai daily-status-email fix — add supporting data | 5:15-5:45pm | - | 0.5 | not started | | |
| 6b | (new, found in mail triage) BNKC-1642: create an Elasticsearch API key with readonly permission — "finish this and reply" | - | - | ? | not started | | |
| 6c | (new, found in mail triage) AO Decision Model Logstash Pipelines — Production Deployment Request from Prathyusha: deploy pipelines to UAT + validate, update Prod credentials, create Prod ES indices, promote to Prod. Target: model components in Prod by 07/28. Ref: PR BZPC-15. **Has a call tonight at 10pm about this.** | 10:00pm call (duration TBC) | 07/28 | ? | not started (call scheduled tonight) | | |
| 7 | Task 4: Confluence AITAPA status update + production dates | 9:30-10:00pm (shortened — 10pm call now in this slot) | - | 1.0 | not started | | |
| 8 | MOM for Tuesday's recorded Elastic call | after the 10pm call | - | 0.75 | not started | | |

**Skilling:** did NOT happen as planned (6:00-7:00pm) — that time went to mail triage instead (see 6-6:25pm below), which is what surfaced the two new tasks above.

**Rolled to Monday 07/20 (as time allows / doesn't fit today):**
- EPLX new skill category — ~4h of KT sessions
- Jira ticket Excel compilation (since Feb 2026) — still deferred, low priority
- Whatever of Task 4/MOM/BNKC-1642/AO Decision Model prep doesn't finish tonight (AO Decision Model has until 07/28, so most of that work rolls forward regardless)
- Confirm whether Thursday's Workspace call (moved from Wednesday) happened — still unconfirmed

**Context — rolled from Tue 07/14 (Wed/Thu unconfirmed, see Yesterday's Brief):**
1. Task 2 — module deployed and working; CMEK blocked on a missing key-vault role.
2. Prisma alerts from Deepak — not yet received as of today; following up.

## Progress Log

(One entry appended per check-in, newest last.)

### 3:00pm check-in

- Checked Notion first — found a direct update: "@12:45pm I had call with Bhumpaka, Sampath" (no duration given, and before today's official 1:00pm start). This is an unplanned call — duration not yet known.
- Sent push notification asking: how long the Sampath Bhumpaka call ran (for the tally), and status on the Deepak/Prisma follow-up and Task 2 (CMEK). Awaiting reply.
- Unplanned-call tally so far today: 1 call (Bhumpaka, Sampath, 12:45pm) / duration pending.
- Next check-in: 5:00pm.

### 5:00pm check-in

- Checked Notion first — found substantial direct updates in the Brain Dump:
  - 12:45pm call with Sampath Bhumpaka: about DI work, he had API questions, redirected to Ravi (Gen AI team). Duration still not given.
  - 1:00-2:00pm: tested a role Heath sent for the key-vault/CMEK errors (`wf_role_assignment_scus_hg41_azure_pe_approver`, "Azure AI Enterprise Network Connection Approver").
  - Got new contacts from Karthik for the Vault issue: Tu Balaji, Avishek Battacharya.
  - Lunch actually ran 2:18-3:18pm (1h, not the planned 2:00-2:30pm slot).
  - After lunch: re-ran and it worked — added an AzureML Data Scientist role too (per Harsha) — Task 2 now largely running. Intermittent Vault issue remains (only works on retry); messaged Avishek about it at 3:40pm.
  - 3:45pm: ad-hoc — helped Karthik create components in AITAPC using the IDP tool (not on the original plan).
- Sent push notification asking: duration of the Sampath call, and whether Task 3 (Prisma tickets)/Phase-2 review/Elastic follow-up got touched or are still pending. Awaiting reply.
- Unplanned-call tally so far today: 1 call (Bhumpaka, Sampath) / duration still pending.
- Next check-in: 7:00pm.

### 7:00pm check-in (before leaving office)

- Checked Notion first — found a lot more direct updates:
  - 4:30pm: informed the Vault issue is known and the team is already working on it (not on the user to chase).
  - 6:00pm (mail review): found a pending Jira ticket **BNKC-1642** — create an Elasticsearch API key with readonly permission, "finish this and reply."
  - Also found a new email from Prathyusha: **AO Decision Model Logstash Pipelines — Production Deployment Request** (deploy to UAT + validate, update Prod credentials, create Prod ES indices, promote to Prod; target model-components-in-Prod date 07/28; PR BZPC-15 has the UAT scripts). **User has a call tonight at 10pm about this.**
  - 6:00-6:25pm: cleared mail and collated info (this replaced the planned 6-7pm skilling hour — skilling didn't happen today).
  - Also pasted for reference (not action items): a Predictive AI platform executive-summary note, and two platform announcements (Tachyon Cortex AutoML on GCP, PULSE lifecycle tool) — logged for context only.
- This new 10pm call collides with the planned Task 4 (9:30-10:30pm) and MOM (10:30-11:15pm) slots — shortened Task 4 to 9:30-10:00pm and pushed MOM to after the call, duration TBC.
- Sent push notification asking: duration of the still-unconfirmed Sampath call, and how long the 10pm call is expected to run so tonight's plan can be adjusted properly. Awaiting reply.
- Unplanned-call tally so far today: 1 call (Bhumpaka, Sampath) / duration still pending. (10pm call is work-related/expected, not counted as "unplanned.")
- Next check-in: 9:30pm, after commute + dinner.

### 9:30pm check-in (post commute/dinner)

- Checked Notion first: no new direct updates since the 7:00pm check-in.
- Sent push notification asking how the day went overall, status on Task 4 (Confluence), and — still outstanding — the Sampath call duration and expected length of tonight's 10pm call. Awaiting reply.
- Unplanned-call tally so far today: 1 call (Bhumpaka, Sampath) / duration still pending.
- Next check-in: 11:15pm (wrap-up).

### 11:15pm wrap-up

- Checked Notion first: no new direct updates since 7:00pm. Sent a final push asking for the Sampath call duration, whether the 10pm call happened (and how long), and status on Task 3/4, Phase-2, Elastic follow-up, Kalai fix, and BNKC-1642. No reply landed before closing this out.

## Day Summary (written at wrap-up)

**Closing on confirmed information only — several items unconfirmed, not fabricating completions.**

- **Task 2 (CMEK validation) — substantial confirmed progress:** tested Heath's role assignment (`wf_role_assignment_scus_hg41_azure_pe_approver`), then after lunch added an AzureML Data Scientist role (per Harsha) too — "back and running." An intermittent Vault issue remains, but at 4:30pm the user was told the platform team already owns it, not something the user needs to chase further. Logging 1.0h (matches the time actually allocated to it across the day).
- **Mail triage (6:00-6:25pm, confirmed):** 0.42h spent clearing mail, which surfaced two new items: Jira BNKC-1642 (create an Elasticsearch API key, readonly) and an AO Decision Model Logstash Pipelines Production Deployment request from Prathyusha (target 07/28, PR BZPC-15) with a call scheduled for 10pm tonight. This replaced the planned skilling hour.
- **Unplanned call (12:45pm) with Sampath Bhumpaka:** confirmed it happened (DI/API questions, redirected to Ravi), but duration was never given despite being asked at all four subsequent check-ins. Logging 0h to the tally — not fabricating a duration.
- **Ad hoc: helped Karthik with AITAPC components (~3:45pm):** confirmed happened, duration unconfirmed — not logged with hours.
- **Unconfirmed / presumed not done — no update at any check-in despite repeated asks:**
  - Task 1 (Deepak/Prisma-alerts follow-up)
  - Task 3 (raise ≥4 Prisma tickets)
  - Phase-2 review + Timothy McDonald
  - Elastic follow-up (verify Sudhir's deployment, status emails)
  - Kalai daily-status-email fix
  - Task 4 (Confluence AITAPA update)
  - MOM for Tuesday's recorded Elastic call
  - BNKC-1642 (Elasticsearch API key)
- **Total confirmed hours today:** 1.0 (Task 2) + 0.42 (mail triage) = **1.42h.** This almost certainly understates real work done (the day was clearly busy — Vault troubleshooting, ad hoc help, mail triage, a scheduled 10pm call) but I'm only logging what has an actual confirmed time span, per the no-fabrication rule.
- **Unplanned calls:** 1 (Bhumpaka, Sampath, 12:45pm) — duration unconfirmed, not counted in hours.

**Update (Mon 07/20, retroactive):** the user confirmed the 10pm AO Decision Model call *did* happen and ran **1.2h**. Adding this as a confirmed row — total for the day revises to **1.42 + 1.2 = 2.62h**. An MOM for this call is now a new task for Monday.

- **Rolled to Monday 07/20 (tomorrow, Saturday, is not a work day):**
  - Task 1 — Deepak/Prisma-alerts follow-up
  - Task 3 — Prisma tickets
  - Phase-2 review + Timothy McDonald
  - Elastic follow-up (verify deployment, status emails)
  - Kalai status-email fix
  - Task 4 — Confluence update
  - MOM — Tuesday's recorded Elastic call
  - MOM — Friday's AO Decision Model call (new, since it's now confirmed it happened)
  - BNKC-1642 — Elasticsearch API key
  - AO Decision Model Logstash Pipelines Prod deployment (target 07/28) — beyond the call itself
  - EPLX KT (~4h), Jira Excel compilation (deferred)
  - Confirm whether Thursday's Workspace call happened — still unconfirmed
  - Wed 07/15 and Thu 07/16 — still pending user backfill (per their own request on 07/17)
- **Final status:** a day with real, confirmed technical progress on Task 2, but most of the original task list remained unconfirmed at wrap-up. The 10pm call outcome was confirmed Monday (happened, 1.2h) and folded in retroactively.
