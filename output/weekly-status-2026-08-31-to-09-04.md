# Weekly Team Status Excel Input — Mon 31 Aug to Fri 4 Sep 2026

**Notion page:** https://app.notion.com/p/3cd7a5e7c4ee81818a88da67b4822688

**Source:** Tasks Tracker (https://app.notion.com/p/3917a5e7c4ee80c99c09f79f3bc68a54) + Projects (https://app.notion.com/p/3917a5e7c4ee80e6bc44f418d6139904) — Project → Task (Jira ticket) → Subtask (daily log). Pull this week's rows from the "This Week (31 Aug-4 Sep)" live view on the Notion weekly page.

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Created at the start of the week per standing instruction; updated daily as hours are logged. Built 2026-08-31.

## Monday, 31 Aug 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 31/08/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 31/08/2026 | NA | AITAPA | Regular Work | AITAPA Azure ML workspace setup — environment/resource configuration work | | 8 | NA | Completed | NA | |

### Tuesday, 1 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 01/09/2026 | NA | Others | Meetings | Daily syncs/standups; CIS team handed off newly-published Terraform module, asked to rebuild resources from the provided example | | 2 | NA | Completed | NA | |
| 01/09/2026 | NA | AITAPA | Regular Work | Recreated AML workspace resources (Nonprod EUS, storage-network config) from the CIS-provided module example | | 5 | NA | Completed | NA | |
| 01/09/2026 | NA | AITAPA | Debugging Sessions | Fixed NSG-related configuration issue and a local configuration error while rebuilding resources | | 2 | NA | Completed | Fixed: NSG config issue; local config error | |

### Wednesday, 2 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 02/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 02/09/2026 | NA | AITAPA | Regular Work | Major refactor and module alignment for AML beta.10 path across workspace/compute/storage/network files | | 4 | NA | Completed | NA | |
| 02/09/2026 | NA | AITAPA | Debugging Sessions | Fixed tag validation, subnet-attribute, missing features-block, storage auth, and AML CMEK/azapi compatibility errors | | 4 | NA | Completed | Fixed: tag validation mismatch; unsupported subnet attribute; missing default azurerm features block; key-based storage auth blocked; CMEK/azapi compatibility issue. Plan now reaches valid state with policy checks passing | |

### Thursday, 3 Sep 2026 (Total: 9 — day in progress)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 03/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 03/09/2026 | NA | AITAPA | Debugging Sessions | Fixed transient Terraform provider download failure (hashicorp/random v3.9.0) due to network reset | | 2 | NA | Completed | Fixed: provider download failure; verified via rerun, plan runs with valid changes | |
| 03/09/2026 | NA | AITAPA | Regular Work | Continued workspace rebuild — resolving branch divergence and staged changes across workspace/compute/storage files | | 6 | NA | In-Progress | One unresolved merge path remains (legacy EUS ML file marked deleted); local and origin/dev branches diverged | |

### Friday, 4 Sep 2026 (Total: TBD)

*(to be filled in)*

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 31/08 | 9 |
| Tue 01/09 | 9 |
| Wed 02/09 | 9 |
| Thu 03/09 | 9 |
| Fri 04/09 | TBD |
| **Week total** | **TBD** |
