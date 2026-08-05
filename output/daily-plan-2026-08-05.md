## Day Summary Header

- **Date:** 2026-08-05 (Wednesday)
- **Notion page:** https://app.notion.com/p/3b37a5e7c4ee81c0aafdfb63a643cf5d
- **Status:** planned (work windows / brain dump not yet locked in)

## Yesterday's Brief (04 Aug 26 — Tuesday)

- 08/04 was spent almost entirely troubleshooting two workbench issues with Basha: the ad-hoc Pooja/i0001 workbench issue, and the broader AITAPA workbench-creation "200 OK"/soft-delete blocker. Neither explicitly confirmed resolved — "tried to troubleshoot" was the user's own framing. No hours given. Recurring calls happened normally afterward.
- **Unconfirmed from 08/04, rolled forward:** Roles setup + Deepak email, 2pm KT call, daily status update, AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation.
- **Today (08/05) is the AITAPA "use-case onboardable" deadline.**
- Standing lower-priority list still open: D001 Production Changes verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook cross-check, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release, Lukens Matthew email, Task 6 Elastic follow-up, Task 8 Leela email, both MOMs, BNKC-1642, AO Decision Model Prod work, EPLX KT, Jira Excel compilation.

## Tasks

| # | Task | AppID | Status |
|---|------|-------|--------|
| 1 | Roles setup + email Deepak — reviewed Copilot's Terraform RBAC refactor (persona-based AML roles, AITAPA) against the AD group/object-ID data on the linked "AITAPA roles" page | AITAPA | **In progress** — strict validity review completed in chat; see findings below. Not yet safe to apply/send to Deepak until the flagged items are resolved. |

## Progress Log

(One entry appended per check-in, newest last.)

### Roles setup — Copilot change review (direct from chat)

Reviewed the "AITAPA roles" linked page (Copilot's Terraform persona-RBAC refactor for AITAPA, parity with the existing GCP AITAPC persona pattern) against the AD group/object-ID data supplied. Findings:

**Critical — must resolve before applying/sending to Deepak:**
1. The "reader" persona's object ID is unconfirmed — only 4 object IDs were ever supplied (platform/IAC, mleng, dsci, RO Console Access); no explicit reader-group object ID was given, yet Copilot's changelog claims a 4-persona map including reader. Need to confirm exactly which object ID Copilot used.
2. No real `terraform plan` was run — only "no syntax issues" from editor diagnostics; `terraform validate` never completed (modules not initialized). Syntax-clean isn't semantically correct — need `terraform init && terraform plan` and a reviewed diff before this goes near prod.
3. Old singleton role-assignment modules were deleted (item 8 in the changelog) on the assumption the new persona map is a strict superset — needs verification via the plan diff that no currently-working access is silently revoked for users not captured by the 4 personas.
4. Compute-instance owner object-id map — unclear whether this was populated with real, current user object IDs or left as placeholders; Copilot's own template asked for real names/IDs that weren't visibly supplied in what's on the page.

**Needs explicit sign-off (read like Copilot's assumptions, not confirmed decisions):**
5. TFE/Vault groups (`DOE.*.TFE.AITAPA`, `TFE_AITAPA_*`, `VAULT_AITAPA_*`) excluded from AML workspace RBAC — consistent with the final persona map, but never explicitly confirmed in writing.
6. Exact role bundle per persona (which of AzureML Data Scientist / Compute Operator / Contributor / Reader each persona gets) — changelog doesn't restate the final table.
7. `DOE.Developer.AITAPA` (object id `b26e2074-11ff-43b6-9070-63c585cb7f6b`) appears in a separate table, disconnected from the main persona list — unclear if/how it's been incorporated.

**Checks out:**
- Correctly rejected the numeric catalog/entitlement IDs (e.g. `16007888`) as unusable for Terraform `principal_id` binding — Azure role assignments need the Azure AD object GUID.
- The 4 supplied GUIDs are well-formed, no obvious typos.
- One-UAMI-per-persona design mirrors the existing GCP service-account-per-persona pattern — reasonable consistency choice.

**Not yet done:** re-engaging Copilot with the above, getting the plan diff, and only then emailing Deepak.

## Day Summary

*(written at wrap-up)*
