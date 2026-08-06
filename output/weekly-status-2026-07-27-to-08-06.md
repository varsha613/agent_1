# Weekly Team Status Excel Input — Mon 27 Jul to Thu 06 Aug 2026

Built 2026-08-06, spanning two work weeks (27-31 Jul fully detailed from the
user's recap + 29 Jul MOM; 03-06 Aug from daily-plan logs, hours largely
unconfirmed — not fabricating durations that were never given). The 09 Jul-dated
"Cert Renewal Deployment (VDB Production)" MOM was uploaded today (08/06) and is
folded into today's row.

## Week 1: Mon 27 Jul – Fri 31 Jul 2026 (Total: 36.0h)

### Monday, 27 Jul 2026 (Total: 9.0h)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 27/07/2026 | NA | Others | Meetings | Combined: India standup + IND AIML sync (extended ~1h25m) + AIML standup + Tachyon DSU + Daily Sync AITAPA | | 3.92 | NA | Completed | NA | No Elastic SME this week |
| 27/07/2026 | NA | Others | KT sessions | KT session — Prisma Alerts walkthrough | | 1.0 | NA | Completed | NA | Given by a colleague; name kept off this sheet, personal reference only |
| 27/07/2026 | NA | Others | KT sessions | Skill-up | | 1.5 | NA | Completed | NA | |
| 27/07/2026 | NA | AITAPC | Debugging Sessions | Light Prisma work | | 0.5 | NA | In-Progress | NA | Estimated split |
| 27/07/2026 | NA | AITAPA | Info for Management | AITAPA docs (continued) | | 0.5 | NA | In-Progress | NA | Estimated split |
| 27/07/2026 | NA | AITAPA | Debugging Sessions | AITAPA work (soft-delete/infra) | | 1.58 | NA | In-Progress | Resolution status clarified 08/03 — see 29/07 row below | Estimated split |

### Tuesday, 28 Jul 2026 — PTO (Total: 0h)

Full-day PTO (sickness). No work expected or logged.

### Wednesday, 29 Jul 2026 (Total: 9.0h)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 29/07/2026 | NA | Others | Meetings | Combined: AIML standup + Tachyon DSU + Workspace call (ran ~1h instead of usual 30min) | | 2.0 | NA | Completed | NA | No Elastic SME this week |
| 29/07/2026 | NA | Others | KT sessions | Skill-up | | 1.5 | NA | Completed | NA | |
| 29/07/2026 | NA | AITAPC | Debugging Sessions | CW pipeline error/failure in prod i0001 — call (Sai Sashank, Rathiesh, Basha, Barghavi) + follow-up work, 5-9pm | | 4.0 | NA | Completed | NA | Call ~1.25h; rest of the 5-9pm block was follow-up work |
| 29/07/2026 | NA | AITAPA | Info for Management | Update "AITAPA Setup Status" doc — practical rewrite matched to Rahul's Phase-1/Phase-2 status email | | 0.5 | NA | Completed | NA | Module version and production dates still flagged as needing real values |
| 29/07/2026 | NA | AITAPC | Debugging Sessions | Prisma alert BLNC-7488 — delete Vertex AI/GCS resources in nonprod-corp-aitapc-d001-48c0 | | 1.0 | NA | Completed | NA | |
| 29/07/2026 | NA | AITAPA | Debugging Sessions | AITAPA Workspace debugging & sync (per MOM) — new "200 OK" masked-failure error blocking compute instance, likely CMEK-policy-related; soft-delete still not resolved despite beta deployment | | 0 | NA | Blocker | Raised high severity with Microsoft; root cause unconfirmed; policy-team ticket pending, no ETA | Found via MOM search 08/03 |

### Thursday, 30 Jul 2026 (Total: 9.0h)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 30/07/2026 | NA | Others | Meetings | Combined: India standup + IND AIML sync + AIML standup + manifestation readiness/AI Cortex AutoML demo (overlapping) + Daily Sync AITAPA | | 3.75 | NA | Completed | NA | No Elastic SME this week |
| 30/07/2026 | NA | Others | KT sessions | Skill-up | | 1.5 | NA | Completed | NA | |
| 30/07/2026 | NA | AITAPC | Debugging Sessions | Workbench issues, i0001 + d0004 (for Puja, Narayesh/Narayan, Devindra) — call with Satyapal, started evening | | 3.5 | NA | In-Progress | Continued into Friday | User-given figure |
| 30/07/2026 | NA | AITAPA | Debugging Sessions | AITAPA workspace work (200 OK / soft-delete blocker follow-up) | | 0.25 | NA | In-Progress | Per 29 Jul MOM blocker, ongoing | Fills the day to 9h, per user's request to add the gap to AITAPA |

### Friday, 31 Jul 2026 (Total: 9.0h)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 31/07/2026 | NA | AITAPC | Debugging Sessions | Workbench issues, i0001 + d0004 (for Puja, Narayesh/Narayan, Devindra) — continued, full day | | 9.0 | NA | Completed | NA | Continued from Thursday evening; whole day per user |

## Week 2 (partial): Mon 03 Aug – Thu 06 Aug 2026 (Total confirmed hours: 0h)

**Note:** no hour breakdowns were given for any day this week — every row below has actual duration unconfirmed. Not fabricating figures; leaving `Total Hours` blank per the no-fabrication rule.

### Monday, 03 Aug 2026

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 03/08/2026 | NA | AITAPC | Debugging Sessions | Workbench issues, i0001 + d0004 — resolved | | | NA | Completed | NA | Root cause: image registry lifecycle policy, 15-image-per-repo limit auto-deleting older images. Duration never given. |

### Tuesday, 04 Aug 2026

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 04/08/2026 | NA | AITAPC | Debugging Sessions | Ad hoc: workbench issue in i0001 for Pooja — troubleshooting with Basha | | | NA | In-Progress | Full resolution not explicitly confirmed | Duration not given; day's main focus |
| 04/08/2026 | NA | AITAPA | Debugging Sessions | Workbench-creation "200 OK" / soft-delete blocker — troubleshooting with Basha | | | NA | In-Progress | High severity, raised with Microsoft; full resolution not explicitly confirmed | Duration not given; day's main focus |

### Wednesday, 05 Aug 2026

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 05/08/2026 | NA | AITAPA | Debugging Sessions | Roles setup (Copilot Terraform RBAC refactor) — two rounds of review posted to Notion | | | NA | In-Progress | Reader-GUID provenance unconfirmed; old-principal access-loss risk unresolved; no terraform plan run yet | Duration not given; not yet safe to send to Deepak |
| 05/08/2026 | NA | AITAPA | Debugging Sessions | Parallel-test working ML instance per 29 Jul MOM interim checklist (dataset, job, pipeline, package install) | | | NA | In-Progress | No results reported back | Steps documented; outcome unconfirmed |

### Thursday, 06 Aug 2026 (today)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 06/08/2026 | NA | Others | Production Calls | Cert renewal deployment call (VDB Production, Elasticsearch) with Sudhir — UCD deploy of renewed cert; keystore error traced to Elastic Config App version mismatch (8.13.2.2 vs 8.13.2.3, activation script hardcoded to 2.2); decided to stay on 8.13.2.2 for this cycle rather than push untested 2.3 to prod | | | NA | Completed | NA | MOM uploaded 08/06; validated post-deployment (services up, indices spot-checked, monitoring re-enable pending). Duration not given. |

## Weekly Summary

| Day | Hours Logged | Basis |
|-----|---------------|-------|
| Mon 27/07 | 9.0 | Per user recap, 3 items split estimated |
| Tue 28/07 | 0 | PTO (sickness) |
| Wed 29/07 | 9.0 | Per user recap + MOM |
| Thu 30/07 | 9.0 | Per user recap + 0.25h AITAPA gap-fill |
| Fri 31/07 | 9.0 | Per user recap |
| **Week 1 total** | **36.0h** | |
| Mon 03/08 | 0 (confirmed) | Workbench fix completed, duration never given |
| Tue 04/08 | 0 (confirmed) | Full day on troubleshooting, duration never given |
| Wed 05/08 | 0 (confirmed) | Roles review + interim testing, duration never given |
| Thu 06/08 | 0 (confirmed) | Cert renewal call completed (MOM confirms), duration never given |
| **Week 2 (partial) total** | **0h confirmed** | Activity happened every day; hours simply weren't reported |
| **Combined 27 Jul – 06 Aug** | **36.0h confirmed** | |

**Still open:** the AITAPA "200 OK" blocker and soft-delete issue remain unresolved (high severity, with Microsoft, no ETA). AITAPA roles/RBAC refactor still not safe to send to Deepak (reader-GUID provenance + old-principal access-loss risk unresolved, no `terraform plan` reviewed). The 29 Jul MOM's interim validation checklist (dataset/job/pipeline/package-install) has no reported results yet. Cert renewal (VDB/Elasticsearch prod) — closed for this cycle on v8.13.2.2; v8.13.2.3 still needs lower-environment testing before a future production push (owner: Sudhir), and Sudhir owes a written follow-up email on the version discrepancy. All other previously-rolled items (Task 6 Elastic follow-up, Task 8 Leela email, both earlier MOMs, Phase-2 review + Timothy McDonald, BNKC-1642, AO Decision Model Prod work, EPLX KT, Jira Excel compilation, 07/21 Workspace-call confirmation, D001 verification, image build statuses, Rathiesh's notebook, GCP Cloud Spanner) are still untouched.

**If you have actual hour totals for 03-06 Aug, give them and I'll fill in the blanks above rather than leave them at 0.**
