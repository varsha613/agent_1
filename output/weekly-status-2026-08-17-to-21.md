# Weekly Team Status Excel Input — Mon 17 Aug to Fri 21 Aug 2026

**Notion page:** https://app.notion.com/p/3bf7a5e7c4ee81159071feb0a26a33ec

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Created at the start of the week per standing instruction; updated daily as hours are logged. Built 2026-08-17.

## Monday, 17 Aug 2026 (Total: TBD)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 17/08/2026 | NA | AITAPA | Debugging Sessions | AML workspace naming/suffix standardization for new workspace instance — updated additional name, friendly name, and description to new target naming set | | TBD | NA | Completed | NA | |
| 17/08/2026 | NA | Others | Meetings | Combined: IND AIML Sync Up + AIADB KT Discussion + AIML Daily Standup + Tachyon Cortex Cloud Pioneers DSU + Daily Sync Tachyon Cortex AI Platforms (AITAPC & AITAPA) | | TBD | NA | Completed | NA | AIML India Team KT Sessions was canceled |

### Tuesday, 18 Aug 2026 (Total: TBD)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 18/08/2026 | NA | AITAPA | Debugging Sessions | Removed stale role-assignment blocks and a duplicate storage outbound private-endpoint rule; added platform_admin RBAC modules (Key Vault Administrator, Azure AI enterprise/network roles) | | TBD | NA | Completed | Fixed: missing RBAC permissions for workspace/network/private-endpoint approval and admin flows | |
| 18/08/2026 | NA | AITAPA | Debugging Sessions | Enabled storage account shared access key (was disabled) to support a workload/integration path requiring key-based storage access | | TBD | NA | Completed | NA | |
| 18/08/2026 | NA | Others | Meetings | Combined: AIADB sync up + Tachyon Cortex Cloud Pioneers DSU + Daily Sync Tachyon Cortex AI Platforms + [3L/ACE] DAUTO Office Hours | | TBD | NA | Completed | NA | |

### Wednesday, 19 Aug 2026 (Total: TBD)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 19/08/2026 | NA | AITAPA | Debugging Sessions | Upgraded storage module version (4.11.1 → 4.13.0) for policy compliance; renamed AML workspace labels/suffixes for naming consistency; corrected invalid RBAC role string (AI Administrator → Azure AI Administrator) | | TBD | NA | Completed | Fixed: policy/compliance mismatch on older storage module version; invalid RBAC role name | |
| 19/08/2026 | NA | AITAPA | Debugging Sessions | Fixed Terraform apply blockers for AML compute and resource-group deletion; added required provider features; corrected storage import resource ID to target RG | | TBD | NA | Completed | Fixed: apply blocked for AML compute; RG deletion blocked; storage import mismatch | |
| 19/08/2026 | NA | AITAPA | Debugging Sessions | Removed hardcoded user/group object IDs from Terraform, replaced with variable- and persona-derived values; added new compute-instance identity variable | | TBD | NA | Completed | Fixed: portability/environment-specific failure risk from hardcoded principal IDs | |
| 19/08/2026 | NA | AITAPA | Debugging Sessions | Replaced hardcoded Vault role with environment-driven role; added outbound FQDN rule for storage blob endpoint connectivity | | TBD | NA | Completed | Fixed: wrong credential role selection; outbound connectivity gap for storage | |
| 19/08/2026 | NA | Others | Meetings | Attended DPE DCT-AIML Platform DevOps and RunOps Team Meeting (1 hour). Also: AIML Daily Standup + Tachyon Cortex Cloud Pioneers DSU + Daily Sync Tachyon Cortex AI Platforms + Tachyon ML Workspace POC (with Harsha) | | 1.0+ | NA | Completed | NA | AIML India Team KT Sessions canceled again |

### Thursday, 20 Aug 2026 (Total: TBD)

*(to be filled in)*

### Friday, 21 Aug 2026 (Total: TBD)

*(to be filled in)*

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 17/08 | TBD |
| Tue 18/08 | TBD |
| Wed 19/08 | TBD |
| Thu 20/08 | TBD |
| Fri 21/08 | TBD |
| **Week total** | **TBD** |
