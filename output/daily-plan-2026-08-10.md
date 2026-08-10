## Day Summary Header

- **Date:** 2026-08-10 (Monday)
- **Notion page:** https://app.notion.com/p/3b87a5e7c4ee8122a4bdc3d996a6e5b7
- **Work windows:** not yet set
- **Status:** planned

## Last Working Day's Brief (07 Aug 26 — Friday)

- **Never confirmed done, now partly resolved:** the day's planned 4 tasks — (1) prep for + attendance at Deepak's 10:30 AM call, (2) the call itself — **confirmed 08/10: this did not happen**, needs fresh scheduling — (3) Prathyusha's ad-hoc AIADB Logstash UAT request (2 conf files, still unconfirmed), (4) workspace-call recap owed from 08/05 (still unconfirmed). The daily page's task table was never updated past "Not started" and no wrap-up was written.
- **Substantially advanced instead:** an ad-hoc Search API Quota increase email thread (Mark Vanderflugt → chain → Kiran → Keshvam) needed Elastic UAT cluster CPU/heap validation for a 8/3 stress test, before a TPM quota bump (2k→5k, prod target 8/14). Built and fixed a Kibana Dev Tools query against `.monitoring-es-*`, got clean aggregated results (UAT had ample headroom — max 50% CPU briefly, heap 27–67%), cross-validated the timezone/date assumption with a 3-day/hourly-ET check (confirmed correct), and drafted a reply. Per Kiran's direction (Teams, 6:27 PM), the reply needs to go to the full original thread with **Sudhir tagged for a sanity check** — drafted, not yet sent.
- **Still pending on that thread:** Sudhir's validation, the equivalent prod-side check, and actually sending the email.
- **Standing lower-priority list, still untouched:** 2pm KT call, daily status update, AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation, D001 Production Changes verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook cross-check, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release, Lukens Matthew email, Task 8 Leela email, both MOMs, BNKC-1642, AO Decision Model Prod work, EPLX KT, Jira Excel compilation.
- **Weekly sheet closed out:** `weekly-status-2026-07-27-to-08-07.md` now covers the full two weeks (27 Jul–07 Aug) with Friday added — hours for 06/08 and 07/08 still need your confirmation.

## Today's Focus

Priority order: (1) Elastic setup for AO (promoted off the standing lower-priority list), (2) Deepak's call — **confirmed it did not happen Friday**, so this is a fresh prep + schedule + attend, not just a recap. Everything else rolls forward behind these two.

## Tasks (detailed, tabular)

| # | Task | Subtasks | AppID | Status |
|---|------|----------|-------|--------|
| 1 | Elastic setup for AO (promoted from rolled-forward list) | Details pending — user to specify scope (AO Decision Model Prod work was the standing item; confirm if this is that, or separate). | AO / AITAPA | Not started |
| 2 | Deepak's call — did not happen Friday, needs fresh prep + scheduling | Re-prep: RBAC roles review (confirm reader-persona GUID, old-principal question), `terraform init`/`plan` if possible, example pipeline run. Then schedule + attend + capture outcomes. | AITAPA | Not started |
| 3 | Prathyusha's AIADB Logstash UAT (rolled from 08/07) | Confirm status — deployed/tested in UAT yet? Ping Prathyusha once done for her verification, then production. | AIADB | Not started |
| 4 | Workspace-call recap (owed from 08/05, rolled 3rd time) | Give the recap so it can finally be logged. | AITAPA | Not started |
| 5 | Search API Quota thread — close out | Send Sudhir sanity-check request to the full thread (drafted, tagged @Sudhir per Kiran's direction). Run the prod-side equivalent of the Elastic capacity check once Sudhir confirms. | Others | Not started |
| 6 | Weekly sheet hours | Confirm actual hours for Thu 06/08 and Fri 07/08 so the weekly sheet total is accurate. | Admin | Not started |
| 7 | Rolled forward (lower priority, as time allows) | 2pm KT call, daily status update, AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation, D001 verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release, Lukens Matthew email, Task 8 Leela email, both MOMs, BNKC-1642, EPLX KT, Jira Excel compilation. | Various | Not started |

## Progress Log

(One entry appended per check-in, newest last.)

### Day set up (direct from chat)

New week. Rolled forward Friday's 4 unconfirmed tasks, the near-done Search API Quota / Elastic thread (Sudhir sanity-check email drafted, needs sending), and the still-untouched standing lower-priority list. Closed out the weekly sheet through Friday 08/07 (`weekly-status-2026-07-27-to-08-07.md`), flagging 06/08 and 07/08 hours as needing confirmation rather than guessing.

### Today's Focus set (direct from chat)

Confirmed: Deepak's 10:30 AM call **did not happen** on Friday (was previously just "unconfirmed" — now known to be a no-go). Reordered today's priorities: (1) Elastic setup for AO — promoted off the standing lower-priority list to top priority, (2) Deepak's call — fresh prep + scheduling needed, not just a recap. Updated the tasks table accordingly; removed "AO Decision Model Prod work" from the lower-priority rolled list since it's now Task 1 (pending user confirmation these are the same item).

## Day Summary

*(written at wrap-up)*
