# Weekly Team Status Excel Input — Mon 28 Sep to Fri 02 Oct 2026

**Notion page:** https://app.notion.com/p/3ec7a5e7c4ee810ebfa7fd688b0da677

**Note:** This weekly sheet is maintained directly (same table template as always) — the Tasks Tracker database (https://app.notion.com/p/3917a5e7c4ee80c99c09f79f3bc68a54) is used for daily-page tracking only, not for weekly rollups.

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Built 2026-10-01 — Mon/Tue reconstructed from general recall (specific day's page had no itemized detail), Wed/Thu drawn from the detailed "01 Oct 26" session notes page.

## Monday, 28 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 28/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 28/09/2026 | NA | AITAPA | Info for Management | Drafted yearly achievement/performance-review summary | | 2 | NA | Completed | NA | Covering AITAPA build-out, AITAPC, and AIADB contributions |
| 28/09/2026 | PBGNN-4862 | AITAPA | Debugging Sessions | AutoML validation / Key Vault CMK blocker — continued follow-up | | 6 | NA | In-Progress | CMK role assignment still blocked on Azure AD replication delay | |

### Tuesday, 29 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 29/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 29/09/2026 | NA | AITAPA | Development | AML workspace CMEK & Container Registry follow-up — continued work | | 8 | NA | In-Progress | NA | |

### Wednesday, 30 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 30/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 30/09/2026 | NA | AITAPA | Debugging Sessions | CMEK configuration investigation & validation (ML workspace + storage) | | 3.5 | NA | Completed | NA | Confirmed storage CMEK correctly configured (msac-asv2-03 passes); root-caused ML workspace CMEK policy failure (msac-mlrn-03) as a stale module-reference false positive, not a real config gap |
| 30/09/2026 | NA | AITAPA | Debugging Sessions | Container Registry troubleshooting | | 2.5 | NA | Completed | Pre-existing ACR resource group created outside Terraform state needs import/destroy + alert config before re-enabling | 5 fix attempts tried; ultimately disabled container_registry.tf due to cascading state conflicts + hard-mandatory Sentinel policy violation (msac-moni-37, empty alert definitions) |
| 30/09/2026 | NA | AITAPA | Development | Created storage CMEK demo module for validation on a fresh resource | | 1.5 | NA | Blocked | Couldn't run terraform plan — blocked by Vault credential failures | Module wf_storage_account_cm_demo |
| 30/09/2026 | NA | AITAPA | Debugging Sessions | Root-caused Vault credential failures blocking all terraform plan/apply | | 0.5 | NA | Completed | NA | Diagnosed as Azure AD replication delay on newly-created service principals (intermittent, ~50% failure rate); blocks all terraform operations at data-source stage |

### Thursday, 01 Oct 2026 (Total: TBD — day in progress)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 01/10/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 01/10/2026 | NA | AITAPA | Documentation | Authored Terraform workflow automation/hardening recommendations | | 1.5 | NA | Completed | NA | 10 high-impact + 5 quick-win ideas: Vault retry logic, pre-flight compliance checks, Sentinel policy scaffolding, CI/CD gates, drift detection, etc. |
| 01/10/2026 | NA | AITAPA | Development | Implemented quick-win automation | | 2 | NA | In-Progress | NA | Makefile (plan/validate/check-policies/audit-drift/clean), policy-alert-mappings.yaml, RUNBOOK-vault-auth-failures.md, pre-commit hook (blocks empty Sentinel alert blocks), .gitignore hardening |

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 28/09 | 9 |
| Tue 29/09 | 9 |
| Wed 30/09 | 9 |
| Thu 01/10 | 4.5 so far (day in progress) |
| Fri 02/10 | TBD |
| **Week total** | **TBD, pending Thu/Fri** |

## Summary

Current state of AITAPA as of Thursday (in progress): confirmed CMEK encryption is correctly configured on both the storage account and the ML workspace — the one failing compliance check turned out to be a false positive from a stale module reference, not a real gap. Container Registry has been temporarily disabled after hitting cascading Terraform state conflicts and a hard-mandatory Sentinel alerting policy violation; a pre-existing ACR resource group outside Terraform state needs to be imported or destroyed, with alert config added, before it can be re-enabled. The team's primary active blocker across all AITAPA Terraform work was root-caused this week: an intermittent Azure AD replication delay on newly-created service principals is causing Vault credential failures at the terraform data-source stage. In response, work has started on hardening the workflow — a Makefile, pre-commit policy checks, a policy-to-alert mapping reference, and a Vault-failure runbook are now in place. The Key Vault CMK role-assignment blocker carried over from last week remains open, still pending Azure AD replication.
