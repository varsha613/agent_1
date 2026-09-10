# Weekly Team Status Excel Input — Mon 7 Sep to Fri 11 Sep 2026

**Notion page:** https://app.notion.com/p/3d47a5e7c4ee81e09179d7efac6b81b5

**Note:** This weekly sheet is maintained directly (same table template as always) — the Tasks Tracker database (https://app.notion.com/p/3917a5e7c4ee80c99c09f79f3bc68a54) is used for daily-page tracking only, not for weekly rollups.

Manager-facing sheet: task, hours, status, blockers only — no internal Notion links or process notes. Created at the start of the week per standing instruction; updated daily as hours are logged. Built 2026-09-07.

## Monday, 7 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 07/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 07/09/2026 | NA | AITAPA | Regular Work | AITAPA AML workspace setup — continued work | | 8 | NA | Completed | NA | |

### Tuesday, 8 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 08/09/2026 | NA | AITAPA | Regular Work | Persona-driven user onboarding for AML compute, datastore, RBAC | | 4 | NA | Completed | NA | Moved compute/datastore/RBAC to per-user provisioning (compute_instance_scus.tf, datastore_blob.tf, iam_scus.tf, user_access_scus.tf, variables.tf) |
| 08/09/2026 | NA | AITAPA | Debugging Sessions | Fixed apply-time error during onboarding rollout | | 1 | NA | Completed | Fixed: principal/permissions and module-behavior issue during apply | |
| 08/09/2026 | PBDWC-3980 | AITAPA | Info for Management | Escalated Azure ML Registry blocker | | 1.5 | NA | Completed | Blocking deployment of remaining resources for testing | Emailed Kelly Amodio, looped in Deepak Kotla requesting prioritization |
| 08/09/2026 | NA | AITAPA | Admin | Reviewed and approved AITAPA/AITAPC pull requests | | 1.5 | NA | Completed | NA | PR #60, #61 (AITAPA) plus multiple AITAPC inferencing/model-dev PRs |
| 08/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |

### Wednesday, 9 Sep 2026 (Total: 9)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 09/09/2026 | PBDWC-3980 | AITAPA | Documentation | Drafted Azure ML Registry security policy exemption request | | 2.5 | NA | Completed | NA | Sent to Deepak Kotla for review; documented business justification, subscription details, mitigations, October release impact; proposed 6-month exemption |
| 09/09/2026 | PBGNN-4862 | AITAPA | Admin | Submitted policy intake for Registry exemption | | 1.5 | NA | Completed | Delays could impact planned October Azure ML onboarding/release | Confirmed submission to Kelly Amodio; attached exemption form |
| 09/09/2026 | NA | AITAPA | Admin | C9 policy mapping for exemption request | | 1 | NA | Completed | NA | Followed up with Harsha Sahay; received required policy references |
| 09/09/2026 | NA | AITAPA | Admin | Reviewed ICAT360 AD validation requirements | | 1 | NA | Completed | NA | Requested by Deepak Kotla; verified dev-environment info availability |
| 09/09/2026 | NA | AITAPA | Admin | Reviewed and approved AITAPC pull requests | | 2 | NA | Completed | NA | PRs #792-796 |
| 09/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |

### Thursday, 10 Sep 2026 (Total: 9 — day in progress)

| Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments |
|------|---------------------|-------|----------|---------------------|-----------|-------------|--------------------|--------|----------|-------------------|
| 10/09/2026 | NA | Others | Meetings | Daily syncs/standups | | 1 | NA | Completed | NA | |
| 10/09/2026 | NA | AITAPA | Admin | KT/Azure coverage planning | | 8 | NA | In-Progress | NA | Request from Shyam Chitgopkar to onboard another engineer; validating entitlements, preparing docs, scheduling KT sessions |

### Friday, 11 Sep 2026 (Total: TBD)

*(to be filled in)*

## Weekly Summary

| Day | Hours Logged |
|-----|---------------|
| Mon 07/09 | 9 |
| Tue 08/09 | 9 |
| Wed 09/09 | 9 |
| Thu 10/09 | 9 |
| Fri 11/09 | TBD |
| **Week total** | **TBD** |

## Summary

* Mon: continued AITAPA AML workspace setup.
* Tue: shipped persona-driven user onboarding (compute/datastore/RBAC per-user provisioning); fixed an apply-time error; escalated the Azure ML Registry blocker (PBDWC-3980); reviewed/approved AITAPA and AITAPC PRs.
* Wed: drafted and submitted the Registry security policy exemption request (PBGNN-4862); completed C9 policy mapping and ICAT360 AD validation review; more AITAPC PR reviews.
* Thu: started KT/coverage planning for AITAPA Azure work at a stakeholder's request.
