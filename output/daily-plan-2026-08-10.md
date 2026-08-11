## Day Summary Header

- **Date:** 2026-08-10 (Monday)
- **Notion page:** https://app.notion.com/p/3b87a5e7c4ee8122a4bdc3d996a6e5b7
- **Work windows:** not yet set
- **Status:** in progress

**This week's status sheet:** `weekly-status-2026-08-10-to-14.md` / https://app.notion.com/p/3b97a5e7c4ee81ebb11ad2b2037ab39c — created at start of week per standing instruction, update daily.

## Standing notes from user (apply going forward)

- **AppID tagging rule:** Elastic-search-related work is always `AIADB`. Azure-related work is `AITAPA`. GCP-related work is `AITAPC`.
- **Weekly status doc purpose:** it's for the manager — tasks, hours spent, and blockers only. Don't add Notion links or other internal-process detail that isn't necessary there. Meta-tasks about maintaining the sheet itself, and items already captured elsewhere (e.g. a MOM), don't get their own row on it.

## Last Working Day's Brief (07 Aug 26 — Friday) — superseded by user's direct updates below

- Search API Quota thread — **marked Completed on Friday** by the user (was tracked as still-pending here; superseded).
- Workspace-call recap — **already logged as a MOM**; no longer an open task, and per the standing note above won't get a row on the weekly status sheet.
- Weekly sheet closed out through Friday 08/07 — hours for 06/08 and 07/08 still need confirmation.

## Today's Focus

Priority order, per the user's own "for tomorrow" note plus the new AITAPA blocker:

1. **AITAPA — resolve the Terraform errors blocking `terraform plan`** (see Task 1 below; blocks other AITAPA work, so goes first).
2. **AO Decision Model / Logstash — BZPC-204**: UAT already validated with Sudhir; next is prod-logic validation + creating the manifest.
3. **AITAPA — stories, roles doc, Harsha ping** (from the user's "for tomorrow" note).
4. **Deepak's call** — still needs fresh scheduling (unresolved since Friday).
5. Rolled-forward lower-priority list, as time allows.

## Tasks (detailed, tabular)

| # | Task | Subtasks | AppID | Status |
|---|------|----------|-------|--------|
| 1 | AITAPA Terraform errors — resolution plan (blocks other AITAPA work) | Priority order: (a) import existing KV key `kvk-eus-sandbox-aitapa-ml-37-2048-st` into state; (b) confirm `Storage Contributor` role definition exists/is in scope (`az role definition list --name "Storage Contributor"`) — check `platform_admin-group` and `platform_admin-uami` role assignments, may need Basha/platform team if the RBAC catalog changed under the new CMEK policy; (c) clean up stale private-endpoint reference `pe-scus-dev-aitapa-ml-56-st-bl` in `rg-scus-sandbox-aitapa-ml` (`terraform state list \| grep ...`, remove from state if not in Azure); (d) purge or recover soft-deleted ML workspace `mlw-eus-sandbox-aitapa-mlp1-217` (recommend purge + recreate clean, since CMEK just went hard-mandatory — avoids carrying forward a pre-CMEK config); then re-run `terraform plan` to confirm clean. | AITAPA | Not started |
| 2 | AO Decision Model / Logstash pipeline — BZPC-204 | Merged with the former "Prathyusha's AIADB Logstash UAT" task — same work. Pipeline changes made → Sudhir approved → UAT validated together with Sudhir (logic checked for discrepancies). Next: validate prod logic, create the manifest. | AIADB | In-Progress |
| 3 | AITAPA — stories, roles doc, Harsha | (a) Send list of upcoming stories, close out after updating stories in Jira. (b) Validate the roles document and send to Deepak and team. (c) Ping Harsha for an update. | AITAPA | Not started |
| 4 | Deepak's call — did not happen Friday, needs fresh prep + scheduling | Re-prep: RBAC roles review (confirm reader-persona GUID, old-principal question), `terraform init`/`plan` if possible (blocked on Task 1 above), example pipeline run. Then schedule + attend + capture outcomes. | AITAPA | Not started |
| 5 | Weekly sheet hours | Confirm actual hours for Thu 06/08 and Fri 07/08 so the weekly sheet total is accurate. Per the standing note above, this stays a local tracking item only — not a row on the manager-facing sheet itself. | Weekly Status | Not started |
| 6a | Rolled forward — AITAPA | AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation. | AITAPA | Not started |
| 6b | Rolled forward — AITAPC | D001 Production Changes verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook cross-check, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release. | AITAPC | Not started |
| 6c | Rolled forward — daily tracking | Daily status update. | Daily-in | Not started |
| 6d | Rolled forward — unassigned/admin | 2pm KT call, Lukens Matthew email, Task 8 Leela email, both MOMs, BNKC-1642, EPLX KT, Jira Excel compilation. | Others | Not started |

**Dropped from active tracking (resolved per user's direct Notion updates):** Search API Quota thread (completed Friday), workspace-call recap (logged as a MOM).

## Context added directly in Notion (08/10, preserved for reference)

**Prathyusha/BZPC-204 conversation:** Prathyusha asked for the two Logstash conf files (`aiad_ao_event-idpfpcf-analytical.conf`, `aiadb_ao_depm-score-events.conf`) to be tested in UAT with index names matching source; gave Jira story [BZPC-204](https://agile-jira.wellsfargo.net/browse/BZPC-204) — "Make Required Logstash Pipeline Changes for Production Kafka Message Format and Validate..." (currently assigned to Prathyusha, offered to reassign to Varsha). Varsha made the pipeline changes, got Sudhir's approval, and validated in UAT together with Sudhir — checked the logic matched with no discrepancies.

**AITAPA Terraform errors (raw, pasted by user):**
- `Error: loading Role Definition List: could not find role 'Storage Contributor'` — on `module.wf_role_assignment_scus_storage["platform_admin-group-Storage Contributor"]` and again on `platform_admin-uami-Storage Contributor`.
- `Error: loading Role Definition List: unexpected status 404` — private endpoint `pe-scus-dev-aitapa-ml-56-st-bl` under RG `rg-scus-sandbox-aitapa-ml` not found, referenced by `module.wf_role_assignment_scus_platform_admin_uami_storage_pe_reader`.
- `Error: A resource with the ID ".../keys/kvk-eus-sandbox-aitapa-ml-37-2048-st/..." already exists` — needs Terraform import, on `module.wf_storage_account_eus_dev_aitapa...wf_key_vault_key_storage_account`.
- `Error: Failed to create/update resource` — ML workspace `mlw-eus-sandbox-aitapa-mlp1-217`: `"status": "Failed"`, `"code": "BadRequest"`, `"message": "Soft-deleted workspace exists. Please purge or recover it."`

The resolution plan for these is captured in Task 1 above (suggested order: KV key import → confirm role definition → PE state cleanup → purge/recreate workspace → `terraform plan`).

## Progress Log

(One entry appended per check-in, newest last.)

### Day set up (direct from chat)

New week. Rolled forward Friday's 4 unconfirmed tasks, the near-done Search API Quota / Elastic thread (Sudhir sanity-check email drafted, needs sending), and the still-untouched standing lower-priority list. Closed out the weekly sheet through Friday 08/07, flagging 06/08 and 07/08 hours as needing confirmation rather than guessing.

### Today's Focus set (direct from chat)

Confirmed: Deepak's 10:30 AM call **did not happen** on Friday. Reordered today's priorities: (1) Elastic setup for AO — promoted to top priority, (2) Deepak's call — fresh prep + scheduling needed, not just a recap.

### Task 1 clarified (direct from chat)

Confirmed: Task 1 (Elastic setup for AO) **is** the standing "AO Decision Model Prod work" item — prod push needed rework, back in UAT.

### AppID accuracy pass (direct from chat)

Fixed generic AppID placeholders throughout the tasks table; split the mixed "Various" bucket into rows by actual app.

### Rebuilt from user's direct Notion updates (direct in Notion, folded in via chat)

User edited the Notion page directly with a substantial amount of new information: (1) confirmed Task 1 (Elastic/AO) and the old Prathyusha AIADB task are the same work, now tracked under Jira BZPC-204 — merged into one task; (2) marked the Search API Quota thread completed Friday and the workspace-call recap as already logged via MOM — both dropped from active tracking; (3) added a standing AppID rule (Elastic→AIADB, Azure→AITAPA, GCP→AITAPC always); (4) clarified the weekly status doc is for the manager — tasks/hours/blockers only, no extra detail, and meta-tasks/already-documented items don't get rows on it; (5) pasted the Prathyusha/BZPC-204 conversation and four AITAPA Terraform errors with an already-drafted resolution plan; (6) left a "for tomorrow" note (now today) listing AIADB tasks (validate prod logic, create manifest) and AITAPA tasks (stories list + Jira close-out, validate roles doc + send to Deepak/team, fix errors, ping Harsha). Rebuilt today's Tasks table and Today's Focus around all of this.

## Day Summary

*(written at wrap-up)*
