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
| 1 | Roles setup + email Deepak — reviewed Copilot's Terraform RBAC refactor (persona-based AML roles, AITAPA) against the AD group/object-ID data on the linked "AITAPA roles" page | AITAPA | **In progress** — two rounds of review done (initial critique + follow-up on Copilot's rebuttal, posted to Notion). Not yet safe to apply/send to Deepak — new GUID-provenance question + access-loss risk still open. |
| 2 | Parallel-test the working ML compute instance against the 29 Jul MOM's interim validation checklist (while the new/CMEK instance is blocked by "200 OK"): create a dataset, run a job against it, build a pipeline, confirm package installation | AITAPA | Started |

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

### Roles setup — round 2 (Copilot's rebuttal reviewed, follow-up posted to Notion)

Copilot responded to the first review with cited Terraform line evidence (`sdlc-locals.tf:40,65-67,157,172,35`; `ml-work-inst.tf:101`; `ml-work-inst-eus.tf:389,437`). Reviewed and posted follow-up directly onto the "AITAPA roles" Notion page. Outcome:

- **Resolved/addressed:** no-plan-run root cause now known (401 on `localterraform.com` module registry, not a skipped step); old singleton modules confirmed removed; TFE/Vault exclusion confirmed in code; role bundle per persona now stated explicitly.
- **New issue raised:** the reader-persona GUID Copilot cites (`eab0b77e-7cbe-4266-9b7e-26f34151786e`) doesn't match any of the 4 GUIDs documented on the Notion page — provenance ("your final mapping message") isn't verifiable from what's there. Flagged for the user to confirm whether that GUID was actually sent to Copilot somewhere outside the page.
- **Still critical:** old principal `11c8690c-5f96-4725-96d0-103ef2a4e27d` is confirmed (by Copilot's own evidence) to be a different GUID from all current persona principals — real access-loss risk on apply unless resolved. Recommended taking Copilot's offered "safety patch" (temporary parallel legacy-RBAC) rather than assuming that principal is dead.
- Compute-owner map: confirmed carried forward from existing config (not invented), but still a placeholder value, not real per-instance owners.
- **Bottom line, still not safe to apply or email Deepak:** need (1) authenticated `terraform init && terraform plan` reviewed, (2) the `11c8690c-...` access question resolved, (3) written confirmation of the reader GUID's origin.

### Task 2 added — parallel testing vs. 29 Jul MOM (direct from chat)

Per the 29 Jul MOM's "Interim Work (While Blocked on Workspace/Instance)" section: while the new CMEK-based workspace/instance was blocked by the "200 OK" error, the agreed interim plan was to validate functionality on the still-working instance in parallel — create a dataset, run a job against it, build a pipeline, and confirm package installation (standard functional checks not dependent on the blocked deployment). Logged as Task 2, started.

**Note before starting:** the 29 Jul MOM also records that the prior working (non-CMEK) workspace had to be deleted within 3 days of a vulnerability finding, and no new instance has come up since ("200 OK" blocker). Confirm which compute instance is actually reachable right now before running these steps — if none is currently up, this checklist can't run until one is, and that itself is worth reporting back on the blocker thread.

**Step-by-step:**

1. **Create a dataset**
   - Confirm the workspace's datastore (storage account/blob container) is registered and reachable from the compute instance.
   - Register a data asset: `az ml data create --name interim-test-data --version 1 --path <storage-path> --type uri_folder --workspace-name <ws> --resource-group <rg>` (or the equivalent `ml_client.data.create_or_update(Data(...))` in the Python SDK v2).
   - Verify it shows up under **Data** in Azure ML Studio.

2. **Run a job against it**
   - Write a minimal script that reads the dataset and prints row count/schema (a smoke test, not real training).
   - Define a command job YAML pointing at the compute instance and the data asset as input; submit with `az ml job create --file job.yml`.
   - Watch status via `az ml job show -n <job-name>` or the **Jobs** tab in Studio; confirm it reaches **Completed** and check `user_logs/std_log.txt` for the expected output.

3. **Build a pipeline**
   - Define a simple 2-step pipeline (e.g. a data-prep step feeding a dummy training step) using a pipeline YAML or the SDK's `@pipeline` decorator.
   - Submit as a pipeline job (`az ml job create --file pipeline.yml` or `ml_client.jobs.create_or_update(pipeline_job)`).
   - Confirm the pipeline graph renders in Studio and both steps complete.

4. **Confirm package installation**
   - Open a terminal on the compute instance (Studio → Compute → instance → Terminal).
   - Install a test package (`pip install <package>`) — this exercises the outbound rules the 08/07 MOM flagged (PyPI write access, storage endpoint, pythonhosted.org).
   - Confirm success with `pip show <package>` and a working import in a notebook kernel; if it fails, check outbound network rule config first before assuming an environment issue.

Report back which of these 4 pass/fail so the MOM's interim-work item can be marked complete or escalated.

## Day Summary

*(written at wrap-up)*
