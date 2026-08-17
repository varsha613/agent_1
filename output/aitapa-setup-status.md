# AITAPA Setup Status

**Notion page:** https://app.notion.com/p/3ac7a5e7c4ee8082bfe1d537ac120872

| Date | Area | Details | Blocker | Action Taken | Status |
|---|---|---|---|---|---|
| 24 Jun 2026 | Phase 1 Foundation Setup | Azure ML Workspace created successfully; Storage Account and Key Vault provisioned and configured; Application Insights integration completed; AMPLS connectivity established; required role assignments configured | Compute Instance creation blocked during Private Endpoint creation; missing `Microsoft.Network/privateDnsZones/join/action` permission required to link to centralized Private DNS Zones | Cloud Ops ticket raised to request required permissions; followed up with networking and Cloud Ops teams for RBAC update | ~~Blocked~~ Completed |
| 01 Jul 2026 | Infrastructure Progress Update | Azure ML Workspace operational; Storage Account and Key Vault configured; Application Insights integration validated; AMPLS connectivity established; required role assignments configured for base level connectivity; Compute Instance creation completed 30 Jun 2026 | Private Endpoint creation pending completion after RBAC update | Continued role-assignment review across components; planned migration to new module source; planned CMEK workspace creation and environment validation activities | Completed |
| 10 Jul 2026 | Testing & Validation | Module Version: `<Update Module Version>`; Compute Instance access validated; basic Python code execution tested successfully; Azure ML Workspace accessibility verified; core infrastructure components functioning as expected; testing completed for currently available components; functional validation sign-off provided | AutoML/Batch Job testing not yet completed; Python package installation validation pending outbound rule addition; end-to-end environment validation pending | Performed functional validation of deployed infrastructure; documented results and testing observations; scheduled remaining validation activities for v1 sign-off | In Progress |
| Planned | Pending Activities | Fine-tune role assignments across components; migrate to new module source; create new ML Workspace with CMEK encryption; validate Python package installation after outbound rule addition; execute AutoML or Batch Job for v1 sign-off; create Batch Endpoints module for Tachyon workloads; obtain separate subscription and approval for ML Registry; complete end-to-end Azure ML environment validation | Dependency on outbound networking updates; ML Registry approval dependency; Batch Endpoint implementation dependency | | In Progress |

**Overall Status (as of 01 Jul 2026 entry):** Azure ML workspace foundation setup is complete. Compute Instance creation has been successfully validated. Remaining activities include module migration, CMEK workspace creation, package installation validation, AutoML/Batch testing, ML Registry setup, and end-to-end sign-off.

---

## Version 2 — Confluence-Ready Format (29 Jul 2026)

*Scope: AITAPA setup and testing (Varsha).*

### Phase 1

| Date | Functionality | Version | Testing | Issues/Observations | Completed |
|---|---|---|---|---|---|
| 24 Jun 2026 | ML Workspace (Workspace + outbound rules) — Storage Account, Key Vault, Application Insights, AMPLS connectivity, role assignments | v1.1.0 | Foundation setup provisioned and configured | Compute Instance creation initially blocked during Private Endpoint creation — missing `Microsoft.Network/privateDnsZones/join/action` permission; Cloud Ops ticket raised, resolved via RBAC update | Yes |
| 01 Jul 2026 | Compute Instance | v1.1.0 | Compute Instance creation completed 30 Jun 2026; workspace confirmed operational | Private Endpoint creation was pending completion after RBAC update — now resolved | Yes |
| 10 Jul 2026 | Featurestore / Core infrastructure validation | v1.1.0 (module version used to be confirmed) | Compute Instance access validated; basic Python code execution tested successfully; Azure ML Workspace accessibility verified; functional validation sign-off provided | AutoML/Batch Job testing not yet completed; Python package installation validation pending outbound rule addition; end-to-end environment validation pending | Yes — Phase 1 components (ML Workspace, Featurestore, Compute Instance) all completed successfully, available on PMR-published v1.1.0 |

### Phase 2

| Date | Functionality | Version | Testing | Issues/Observations | Completed |
|---|---|---|---|---|---|
| 29 Jul 2026 | Compute Cluster | v1.2.0-beta.4 | Beta published | No issues reported | Yes (Beta) |
| 29 Jul 2026 | Registry | — | In-progress | Separate subscription and approval pending for ML Registry | No |
| 29 Jul 2026 | Batch Endpoint | — (Beta) | Beta version published | "Deployments" feature still in-progress; Batch Endpoints module for Tachyon workloads pending | Partial — beta published, Deployments feature in-progress |
| 29 Jul 2026 | Datastore | v1.2.0-beta.4 | Beta published | No issues reported | Yes (Beta) |

### Production Dates

| Item | Target Date |
|---|---|
| AITAPA use-case onboardable target | **[to be confirmed]** |
| v1 sign-off (post AutoML/Batch testing) | **[to be confirmed]** |

### Current Blocker (from 29 Jul 2026 MOM — Tachyon Cortex / AITAPA Workspace Debugging & Sync)

**"200 OK" error — primary blocker.** Workspace update calls return a "200 OK" response that is actually masked failure — the compute instance no longer comes up after the latest version update, even though workspace creation itself succeeds. Likely linked to the CMEK policy being made hard-mandatory on the 15th (multiple team members have seen this since the 16th). Raised as high severity with Microsoft; root cause not yet confirmed. AKS version upgrade ruled out as the cause. Team requesting the CMEK policy be reverted to soft-mandatory temporarily to isolate whether CMEK is the actual cause — ticket filed with the policy team, no confirmed ETA (rough estimate: a couple of days once actioned).

**Soft delete — still not resolved.** Soft delete support was added and deployed in beta (v0.9.1.2.2), but deleted workspaces are still appearing under "recently deleted," and workspace-renaming prompts persist despite this. To be raised with Microsoft (Michael, Brian) — open question whether this is a cyber requirement, a missing role, or a CMEK configuration issue. The latest Azure ML workspace tag reportedly includes the soft-delete-enabled option but needs validation.

**Also noted:** a running non-CMEK workspace had to be deleted after being flagged for removal within 3 days due to vulnerabilities — unable to bring a new instance up since. Interim work while blocked: AD group/persona-based access setup (3 personas: Data Scientist, ML Engineer, Prod Support), dataset creation, job run, pipeline creation, and package installation validation on the compute instance — none of these are dependent on the blocked deployment. The Wells Fargo KBK module hit the same "200 OK" issue, confirming it isn't isolated to one module.

**Overall Status (as of 03 Aug 2026 update):** Azure ML workspace foundation setup (Phase 1) is complete and validated. Phase 2 components are progressing — Compute Cluster and Datastore are beta published, Batch Endpoint is beta published with Deployments in-progress, and Registry remains in-progress pending subscription/approval. However, a new primary blocker emerged 29 Jul: a "200 OK" masked-failure error preventing compute instances from coming up, likely tied to CMEK policy enforcement — raised as high severity with Microsoft, root cause not yet confirmed. Soft delete remains unresolved despite a beta deployment. Remaining Phase 1 activities include module migration, package installation validation, AutoML/Batch testing, and end-to-end sign-off.

---

## Version 3 — Persona RBAC Migration Progress (13 Aug 2026 update)

*No new formal MOM has been posted since 29 Jul — the "MoM: AITAPA workspace" page is unchanged. This update reflects real progress captured directly through daily work logs (08/07–08/13), which is the most current AITAPA status available.*

### Persona-based RBAC migration (SCUS)

- **07 Aug:** All 4 persona AD group GUIDs confirmed (`platform_admin`, `ml_engineer`, `data_scientist`, `reader`) — the last one (`reader` = `AZURE_AITAPA_READERS`) verified directly from the Azure console. Persona-based Terraform code written: `locals.personas` map, per-persona UAMI (`for_each`), per-persona role-assignment modules (replacing ~30 hand-copied blocks). `terraform init` blocker (401 on module registry) resolved. SCUS outbound-rules gap found and fixed (was blocking `pip install` under `AllowOnlyApprovedOutbound`). Sandbox test round planned: CMEK temporarily decoupled (not removed) to isolate and test the persona RBAC changes — required for closing a Prisma finding, must be re-enabled before this is called done.
- **10–12 Aug:** Applying the persona RBAC changes surfaced real Terraform errors:
  - **Root cause found + fixed:** SCUS ML workspace creation was failing with a `ValidationError` from a duplicate outbound rule pointing at the same Storage blob destination — removed the duplicate.
  - **Fixed:** a naming mismatch on the SCUS private-endpoint Reader role assignment (scope construction corrected in `role_assgn.tf`).
  - **Fixed:** missing SCUS and EUS role assignments identified via audit and filled in.
  - **New blocker (open):** the EUS Key Vault key import requires a Vault token — `VAULT_ADDR` is set but `VAULT_TOKEN` is not, blocking `terraform import` for the existing KV key.
  - **New, blocked:** a request to rename the EUS ML workspace came in — not yet actioned, exact target name not specified.
- **12 Aug:** AITAPA workspace call held. MOM located 08/13 — see below.

### Workspace call MOM — located 08/13 (17 Aug update)

Titled "MoM: 30/07/26 - AITAPA workspace" in Notion but content clearly describes the recent CMEK/persona debugging work. Attendees: Varsha, Harsha, Deepak (joined mid-call). Key facts:
- **CMEK cannot simply be removed** — Harsha clarified the workspace must be destroyed and recreated to remove it; Varsha had done this, will retry.
- **Microsoft reproduced the "200 OK" error internally for the first time** — suspect an API bug, not confident of root cause.
- **Microsoft's proposed workaround** (Terraform `lifecycle { ignore_changes }`) avoids triggering the error on plan/apply, but would also suppress the legitimate workspace updates Varsha still needs to make — **doesn't actually unblock her.** Agreed to pursue a **Prisma Alert exemption** instead (Deepak → Rahul → Prisma team), independent of the workaround's outcome.
- Outbound rule to the storage account's private endpoint, and UAMI permissions, both flagged as needing validation for dataset creation to work.
- Per-location soft-delete workspace limit (~5) — three workspaces were sitting in soft-delete at the time of the call.
- **Varsha may be missing one of the persona roles Harsha shared** — flagged for checking (see Task 5 on the 17 Aug daily page).
- A dedicated working session was scheduled to go deep on roles/personas + CMEK together with live debugging.

### Open items carried from the architecture review

- Confirm Harsha's role-bundle → persona mapping (her "UAMI Roles" / "User Roles" split) — pending her input.
- Confirm the group-vs-UAMI role-split design call (same bundle to both, or separate lists).
- Decide EUS's long-term fate — it exists only as a SCUS capacity-overflow instance, not a designed second region, and has now hit soft-delete twice.
- Once persona RBAC is validated in the SCUS sandbox, **re-enable CMEK before calling this done** — explicitly tracked so it isn't skipped.
- **New (17 Aug):** pursue the Prisma Alert exemption path (Deepak/Rahul) rather than relying on Microsoft's `ignore_changes` workaround, which doesn't solve the underlying problem.
- **New (17 Aug):** check for the possibly-missing persona role flagged in the newly-found MOM.

**Overall Status (17 Aug 2026):** The persona-based RBAC migration for SCUS is actively in progress — real Terraform errors are being worked through as the code gets applied, with steady resolution but one open blocker (`VAULT_TOKEN`) still stopping the KV key import, plus a pending EUS rename request and a possibly-missing persona role. The "200 OK"/soft-delete saga from the 29 Jul MOM is now better understood via the newly-located 08/13 MOM: Microsoft has reproduced the error but not root-caused it, their proposed workaround doesn't actually help, and a Prisma Alert exemption is the current path forward. Deepak's call has now been missed **3 times** — worth a different scheduling approach.
