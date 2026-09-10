# Weekly Team Status Excel Input — Mon 31 Aug to Fri 4 Sep 2026

**Notion page:** https://app.notion.com/p/3cd7a5e7c4ee81818a88da67b4822688

**Note:** This weekly sheet is maintained directly (same table template as always) — the Tasks Tracker database (https://app.notion.com/p/3917a5e7c4ee80c99c09f79f3bc68a54) is used for daily-page tracking only, not for weekly rollups.

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Created at the start of the week per standing instruction; updated daily as hours are logged. Built 2026-08-31.

## Monday, 31 Aug 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 31/08/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 31/08/2026 | NA | AITAPA | Regular Work | AITAPA Azure ML workspace setup | | 8 | NA | Completed | NA | Environment/resource configuration work |

### Tuesday, 1 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 01/09/2026 | NA | Others | Meetings | Daily syncs/standups + CIS module handoff | | 2 | NA | Completed | NA | CIS team handed off newly-published Terraform module; asked to rebuild resources from the provided example |
| 01/09/2026 | NA | AITAPA | Regular Work | Recreated AML workspace resources from CIS module | | 5 | NA | Completed | NA | Nonprod EUS, storage-network config rebuilt from the CIS-provided example |
| 01/09/2026 | NA | AITAPA | Debugging Sessions | Fixed NSG + local config errors | | 2 | NA | Completed | Fixed: NSG config issue; local config error | |

### Wednesday, 2 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 02/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 02/09/2026 | NA | AITAPA | Regular Work | Major refactor for AML beta.10 module path | | 4 | NA | Completed | NA | Aligned workspace/compute/storage/network files |
| 02/09/2026 | NA | AITAPA | Debugging Sessions | Fixed multiple Terraform plan errors | | 4 | NA | Completed | Fixed: tag validation mismatch; unsupported subnet attribute; missing default azurerm features block; key-based storage auth blocked; CMEK/azapi compatibility issue. Plan now reaches valid state with policy checks passing | |

### Thursday, 3 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 03/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 03/09/2026 | NA | AITAPA | Debugging Sessions | Fixed transient provider download failure | | 2 | NA | Completed | Fixed: provider download failure (hashicorp/random v3.9.0, network reset); verified via rerun, plan runs with valid changes | |
| 03/09/2026 | NA | AITAPA | Regular Work | Continued workspace rebuild | | 6 | NA | In-Progress | One unresolved merge path remains (legacy EUS ML file marked deleted); local and origin/dev branches diverged | |

### Friday, 4 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 04/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 04/09/2026 | NA | AITAPA | Testing | Azure ML workspace deployment validation | | 8 | NA | Completed | NA | Confirmed workspace + compute instance deployed; module v1.2.0-beta.10 resolved the prior issue; began testing workspace functionality |

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 31/08 | 9 |
| Tue 01/09 | 9 |
| Wed 02/09 | 9 |
| Thu 03/09 | 9 |
| Fri 04/09 | 9 |
| **Week total** | **45** |

## Summary

* Mon: continued AITAPA Azure ML workspace setup.
* Tue: CIS handed off a new Terraform module; rebuilt workspace resources from it; fixed NSG and local config errors.
* Wed: major refactor for AML beta.10 path; fixed tag/subnet/features-block/storage-auth/CMEK errors — plan now valid.
* Thu: fixed a transient provider failure; workspace rebuild continuing, one merge conflict outstanding.
* Fri: workspace + compute instance deployment confirmed; module v1.2.0-beta.10 resolved the outstanding issue; began functional testing.
