# Weekly Team Status Excel Input — Mon 21 Sep to Fri 25 Sep 2026

**Notion page:** https://app.notion.com/p/3e57a5e7c4ee816894dee5eac335d933

**Note:** This weekly sheet is maintained directly (same table template as always) — the Tasks Tracker database (https://app.notion.com/p/3917a5e7c4ee80c99c09f79f3bc68a54) is used for daily-page tracking only, not for weekly rollups.

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Built 2026-09-24.

## Monday, 21 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 21/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 21/09/2026 | NA | AITAPA | Debugging Sessions | Fixed datastore authentication identity | | 3 | NA | Completed | Fixed: switched datastore identity type from WorkspaceSystemAssignedIdentity to the workspace's UserAssignedIdentity, resolving AutoML "Not Found" auth failure | |
| 21/09/2026 | NA | AITAPA | Development | Added workspace UAI RBAC and DNS zone config; deployed per-user datastores | | 4 | NA | Completed | NA | Updated iam_scus.tf, DNS zone module, datastore_blob.tf for per-user datastore provisioning |
| 21/09/2026 | PBGNN-4862 | AITAPA | Debugging Sessions | Key Vault CMK role assignment — blocked | | 1 | NA | In-Progress | Key Vault CMK role assignment blocked by Azure AD replication delay (PrincipalNotFound error) | |

### Tuesday, 22 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 22/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 22/09/2026 | NA | AITAPA | Debugging Sessions | Fixed default workspace datastore for AutoML cache | | 8 | NA | Completed | Fixed: default workspace datastore (WORKSPACE_BLOB_DATASTORE) wasn't correctly wired for AutoML cache storage | Module wf_machine_learning_datastore_blob_workspace_default |

### Wednesday, 23 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 23/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 23/09/2026 | NA | AITAPA | Development | Set up Azure Container Registry (ACR) with RBAC | | 8 | NA | Completed | NA | container_registry.tf; AcrPull/AcrPush RBAC; upgraded module v1.2.0-beta.10 → v1.2.0-beta.11 |

### Thursday, 24 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 24/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 24/09/2026 | NA | AITAPA | Documentation | Compiled AITAPA component status inventory | | 3 | NA | Completed | NA | |
| 24/09/2026 | PBGNN-4862 | AITAPA | Debugging Sessions | Continued AutoML job validation | | 5 | NA | In-Progress | CMK role assignment still blocked on Azure AD replication delay | |

### Friday, 25 Sep 2026 (Total: TBD)

*(to be filled in)*

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 21/09 | 9 |
| Tue 22/09 | 9 |
| Wed 23/09 | 9 |
| Thu 24/09 | 9 |
| Fri 25/09 | TBD |
| **Week total** | **TBD** |

## Summary

Current state of AITAPA as of Thursday: root-caused and fixed the AutoML "Not Found" datastore-identity issue found during workshop follow-up — datastore auth now uses the workspace's UserAssignedIdentity, UAI RBAC/DNS zone config and per-user datastores are deployed, and the default workspace datastore is correctly wired for AutoML cache storage. Azure Container Registry has been stood up with RBAC on module v1.2.0-beta.11. Remaining open item: Key Vault CMK role assignment is still blocked by an Azure AD replication delay (PrincipalNotFound); AutoML job validation is continuing in the meantime.
