# Weekly Team Status Excel Input — Mon 14 Sep to Fri 18 Sep 2026

**Notion page:** https://app.notion.com/p/3e57a5e7c4ee8185af52d8b7a7cb9fa6

**Note:** This weekly sheet is maintained directly (same table template as always) — the Tasks Tracker database (https://app.notion.com/p/3917a5e7c4ee80c99c09f79f3bc68a54) is used for daily-page tracking only, not for weekly rollups.

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Built retroactively 2026-09-24 from Tasks Tracker entries.

## Monday, 14 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 14/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 14/09/2026 | NA | AITAPA | Development | Workshop preparation — environment readiness for Microsoft-led AML workshop | | 8 | NA | Completed | NA | |

### Tuesday, 15 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 15/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 15/09/2026 | NA | AITAPA | Learning | Azure ML MLOps enablement workshop (Microsoft) — Day 1 | | 8 | NA | Completed | NA | Covered compute/environments/endpoints/registries/MLflow topics |

### Wednesday, 16 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 16/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 16/09/2026 | NA | AITAPA | Learning | Azure ML MLOps enablement workshop (Microsoft) — Day 2 | | 8 | NA | Completed | NA | Feature store, model registration/promotion, Device Trust GCP→Azure migration exercise |

### Thursday, 17 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 17/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 17/09/2026 | NA | AITAPA | Documentation | Documented workshop session notes and summary | | 8 | NA | Completed | NA | Wrote up Day 1 + Day 2 notes and a 5-point verbal summary for manager call |

### Friday, 18 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 18/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 18/09/2026 | NA | AITAPA | Debugging Sessions | Diagnosed AutoML "Not Found" error | | 8 | NA | Completed | Root cause found: datastore configured with WorkspaceSystemAssignedIdentity, but workspace only has a UserAssignedIdentity (no system MSI) — AutoML couldn't authenticate, returned 404 | |

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 14/09 | 9 |
| Tue 15/09 | 9 |
| Wed 16/09 | 9 |
| Thu 17/09 | 9 |
| Fri 18/09 | 9 |
| **Week total** | **45** |

## Summary

Current state of AITAPA as of end of week: completed a two-day Microsoft-led Azure ML MLOps enablement workshop covering compute/environments, endpoints, model/feature registries, MLflow, feature store, and a GCP→Azure model-migration exercise, with session notes documented for the team. Immediately applying that knowledge, began investigating an AutoML "Not Found" error in the AML workspace and root-caused it to a datastore identity mismatch — the datastore was configured to use WorkspaceSystemAssignedIdentity while the workspace only has a UserAssignedIdentity, so AutoML authentication was failing. Fix is queued for next week.
