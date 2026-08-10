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

Priority order: (1) AO Decision Model — Elastic setup, reworking in UAT after the prod push needed rework (this is the standing "AO Decision Model Prod work" item — confirmed same task), (2) Deepak's call — **confirmed it did not happen Friday**, so this is a fresh prep + schedule + attend, not just a recap. Everything else rolls forward behind these two.

## Tasks (detailed, tabular)

| # | Task | Subtasks | AppID | Status |
|---|------|----------|-------|--------|
| 1 | AO Decision Model — Elastic setup (UAT rework) | For this use case to reach prod, the prod-work task needed rework — it's back in UAT. Elastic setup is the current focus of that rework. Confirmed same item as the standing "AO Decision Model Prod work." Further subtasks pending user's specifics. | AO | Not started |
| 2 | Deepak's call — did not happen Friday, needs fresh prep + scheduling | Re-prep: RBAC roles review (confirm reader-persona GUID, old-principal question), `terraform init`/`plan` if possible, example pipeline run. Then schedule + attend + capture outcomes. | AITAPA | Not started |
| 3 | Prathyusha's AIADB Logstash UAT (rolled from 08/07) | Confirm status — deployed/tested in UAT yet? Ping Prathyusha once done for her verification, then production. | AIADB | Not started |
| 4 | Workspace-call recap (owed from 08/05, rolled 3rd time) | Give the recap so it can finally be logged. | AITAPA | Not started |
| 5 | Search API Quota thread — close out | Send Sudhir sanity-check request to the full thread (drafted, tagged @Sudhir per Kiran's direction). Run the prod-side equivalent of the Elastic capacity check once Sudhir confirms. | Others | Not started |
| 6 | Weekly sheet hours | Confirm actual hours for Thu 06/08 and Fri 07/08 so the weekly sheet total is accurate. | Weekly Status | Not started |
| 7a | Rolled forward — AITAPA | AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation. | AITAPA | Not started |
| 7b | Rolled forward — AITAPC | D001 Production Changes verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook cross-check, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release. | AITAPC | Not started |
| 7c | Rolled forward — daily tracking | Daily status update. | Daily-in | Not started |
| 7d | Rolled forward — unassigned/admin | 2pm KT call, Lukens Matthew email, Task 8 Leela email, both MOMs, BNKC-1642, EPLX KT, Jira Excel compilation. | Others | Not started |

**AppID note (user requested accuracy pass, 08/10):** Row 7d's items don't have a confirmed app owner in anything documented so far — `BNKC-1642`, the Lukens Matthew email, and the Leela email are genuinely unclear (could be AITAPA/AITAPC/AIADB or something outside all three); marked `Others` rather than guessed. Flag if any of these actually belong to a specific app so this can be corrected.

## Progress Log

(One entry appended per check-in, newest last.)

### Day set up (direct from chat)

New week. Rolled forward Friday's 4 unconfirmed tasks, the near-done Search API Quota / Elastic thread (Sudhir sanity-check email drafted, needs sending), and the still-untouched standing lower-priority list. Closed out the weekly sheet through Friday 08/07 (`weekly-status-2026-07-27-to-08-07.md`), flagging 06/08 and 07/08 hours as needing confirmation rather than guessing.

### Today's Focus set (direct from chat)

Confirmed: Deepak's 10:30 AM call **did not happen** on Friday (was previously just "unconfirmed" — now known to be a no-go). Reordered today's priorities: (1) Elastic setup for AO — promoted off the standing lower-priority list to top priority, (2) Deepak's call — fresh prep + scheduling needed, not just a recap. Updated the tasks table accordingly; removed "AO Decision Model Prod work" from the lower-priority rolled list since it's now Task 1 (pending user confirmation these are the same item).

### Task 1 clarified (direct from chat)

Confirmed: Task 1 (Elastic setup for AO) **is** the standing "AO Decision Model Prod work" item — for this use case to reach production, there was a prod-work task, but it needed rework, so it's back in UAT. The Elastic setup is the current focus of that UAT rework, working back toward prod. Updated Task 1's description accordingly.

### AppID accuracy pass (direct from chat)

User asked for accurate AppID tagging throughout: AITAPA/AITAPC/AIADB/AO where the content is clearly about that app, `Weekly Status` for tasks about maintaining the weekly sheet, `Daily-in` for tasks about the daily page/tracking itself. Fixed: Task 1 → `AO` (was the combined "AO / AITAPA"); Task 6 → `Weekly Status` (was `Admin`); Task 7's mixed "Various" bucket split into 4 rows by actual AppID (7a AITAPA, 7b AITAPC, 7c Daily-in, 7d Others) instead of one vague catch-all. Three items in 7d (`BNKC-1642`, Lukens Matthew email, Leela email) don't have a confirmed app owner anywhere in the docs — flagged rather than guessed.

## Day Summary

*(written at wrap-up)*
