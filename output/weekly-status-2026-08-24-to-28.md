# Weekly Team Status Excel Input — Mon 24 Aug to Fri 28 Aug 2026

**Notion page:** https://app.notion.com/p/3c67a5e7c4ee8180bde2d3b6ed9b88fc

**Note:** This weekly sheet is maintained directly (same table template as always) — the Tasks Tracker database (https://app.notion.com/p/3917a5e7c4ee80c99c09f79f3bc68a54) is used for daily-page tracking only, not for weekly rollups.

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Created at the start of the week per standing instruction; updated daily as hours are logged. Built 2026-08-24.

## Monday, 24 Aug 2026 (Total: TBD)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 24/08/2026 | NA | AIADB | Debugging Sessions | aidbqa tenant storage incident (92.9% full) | | TBD | NA | In-Progress | Tenant-to-cluster mapping unconfirmed | Top priority; investigating root cause and remediation |
| 24/08/2026 | NA | AIADB | Debugging Sessions | VDB dev Kibana access error investigation | | TBD | NA | In-Progress | Still reproducing; started Thu 20 Aug evening | Began investigating, reviewed prior troubleshooting; second priority behind storage |
| 24/08/2026 | NA | AITAPA | Debugging Sessions | Testing Azure sample example (AITAPA) | | TBD | NA | In-Progress | Sample causing issues | Fixing underlying architecture |
| 24/08/2026 | NA | Others | Meetings | Team status + skills/capability planning call | | TBD | NA | Completed | NA | Gave status update; confirmed storage-first priority; manager requested a skills/capability learning list from the team |
| 24/08/2026 | NA | AIADB | Info for Management | Drafted skills/capability learning list for manager | | TBD | NA | Completed | NA | Covers what to learn + why, for manager review |

### Tuesday, 25 Aug 2026 (Total: TBD)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 25/08/2026 | NA | AIADB | Debugging Sessions | VDB dev Kibana access error — deep investigation | | TBD | NA | In-Progress | Awaiting SME response; a superuser-vs-regular-user access discrepancy still needs reconciling | Narrowed likely root cause to a duplicate system-index record; escalated to SME for guidance |

### Wednesday, 26 Aug 2026 (Total: TBD)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 26/08/2026 | NA | AIADB | Debugging Sessions | VDB dev Kibana access error — SME escalation | | TBD | NA | In-Progress | Awaiting SME response | Confirmed email sent to SME requesting guidance |
| 26/08/2026 | NA | AIADB | Info for Management | Documented MOM for architecture review meeting | | TBD | NA | Completed | NA | Meeting attended Tue 25 Aug — fraud-detection model, feature-store migration |
| 26/08/2026 | NA | AIADB | Info for Management | Updated learning-scope submission to manager | | TBD | NA | Completed | NA | Updated based on architecture review findings |
| 26/08/2026 | NA | AITAPA | Documentation | Compiled roles/access-setup summary + terminology | | TBD | NA | Completed | NA | For team review |

### Thursday, 27 Aug 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 27/08/2026 | NA | AIADB | Regular Work | Cert cleanup in production — manifest creation | | 0.75 | NA | Completed | NA | |
| 27/08/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 27/08/2026 | NA | AITAPA | Regular Work | AITAPA Azure ML workspace setup | | 7.25 | NA | Completed | NA | Environment/resource configuration work |

### Friday, 28 Aug 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 28/08/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 28/08/2026 | NA | AITAPA | Regular Work | AITAPA Azure ML workspace setup | | 8 | NA | Completed | NA | Environment/resource configuration work |

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 24/08 | TBD |
| Tue 25/08 | TBD |
| Wed 26/08 | TBD |
| Thu 27/08 | 9 |
| Fri 28/08 | 9 |
| **Week total** | **TBD** |

## Summary

* Investigated the aidbqa tenant storage incident (92.9% full) across two Elasticsearch clusters (llds ~4.3TB, vdb-uat ~425GB); found the alert is on a StorageGRID tenant rather than a raw ES metric, and identified reclaim candidates (~2TB of duplicate re-run indices, ~800GB of stale snapshots) — tenant-to-cluster mapping still needs confirming.
* Root-caused the VDB dev Kibana access error to a duplicate system-index record; escalated to the Elastic SME for guidance before any remediation; a superuser-vs-regular-user access discrepancy still needs reconciling.
* Attended and documented the NDDA fraud-detection architecture review, which confirmed Elasticsearch is being retired in favor of MongoDB as the online feature store.
* Submitted and then updated a skills/capability learning-scope list (Elasticsearch/MongoDB, Python) to manager, incorporating the architecture review findings.
* Compiled a persona-based RBAC roles/access-setup summary and terminology reference for team review.
* AITAPA: tested an Azure sample example and worked on fixing the underlying architecture; separately completed cert cleanup in production (manifest creation) and general AML workspace environment/resource configuration work.
