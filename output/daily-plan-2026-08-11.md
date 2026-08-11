## Day Summary Header

- **Date:** 2026-08-11 (Tuesday)
- **Notion page:** https://app.notion.com/p/3b97a5e7c4ee81f6b3ebd31186b8108b
- **Work windows:** not yet set
- **Status:** planned

**This week's status sheet:** `weekly-status-2026-08-10-to-14.md` / https://app.notion.com/p/3b97a5e7c4ee81ebb11ad2b2037ab39c — Monday's row still has hours marked TBD (never confirmed); update once known.

## Standing notes from user (carried forward)

- **AppID tagging rule:** Elastic-search-related work is always `AIADB`. Azure-related work is `AITAPA`. GCP-related work is `AITAPC`.
- **Weekly status doc purpose:** manager-facing — tasks, hours, blockers only. No internal Notion links/process notes. Meta-tasks and items already documented elsewhere (e.g. a MOM) don't get their own row.

## Yesterday's Brief (10 Aug 26 — Monday)

Monday's page (`daily-plan-2026-08-10.md`) was never wrapped up — no Day Summary was written and every task in the table still shows "Not started" or "In-Progress." Nothing here is confirmed done; rolling all of it forward rather than assuming progress that wasn't reported.

- **AITAPA Terraform errors — resolution plan (blocks other AITAPA work):** import KV key `kvk-eus-sandbox-aitapa-ml-37-2048-st` into state; confirm `Storage Contributor` role definition exists/is in scope; clean up stale private-endpoint reference `pe-scus-dev-aitapa-ml-56-st-bl`; purge/recreate soft-deleted ML workspace `mlw-eus-sandbox-aitapa-mlp1-217`; then re-run `terraform plan`. Status unknown — not confirmed whether any of this was actually done Monday.
- **AO Decision Model / Logstash — BZPC-204:** was "In-Progress" — UAT already validated with Sudhir as of Monday morning; next steps were prod-logic validation + creating the manifest. Status since then unconfirmed.
- **AITAPA — stories, roles doc, Harsha ping:** send upcoming stories list + close out Jira, validate roles doc and send to Deepak/team, ping Harsha. Not confirmed done.
- **Deepak's call:** still needed fresh scheduling as of Monday (didn't happen Friday either). Not confirmed done.
- **Rolled-forward lower-priority list:** unchanged, still untouched (6a AITAPA, 6b AITAPC, 6c Daily-in, 6d Others — see Monday's page for full breakdown).

## Today's Focus

*(not yet set — waiting on today's brain dump / confirmation of what actually happened Monday)*

## Tasks (detailed, tabular)

| # | Task | Subtasks | AppID | Status |
|---|------|----------|-------|--------|
| 1 | AITAPA Terraform errors — resolution plan (rolled from 08/10) | Confirmed still unresolved as of Monday — actively being worked on now. Priority order: KV key import → Storage Contributor role check → private-endpoint state cleanup → purge/recreate soft-deleted EUS workspace → `terraform plan`. | AITAPA | In-Progress |
| 2 | AO Decision Model / Logstash — BZPC-204 (rolled from 08/10) | Confirm status — was prod-logic validation / manifest creation done Monday? | AIADB | Not started |
| 3 | AITAPA — stories, roles doc, Harsha (rolled from 08/10) | Game plan built with 9 proposed Jira stories (see Progress Log). Stories list drafted for Scrum Master (not Harsha); separate role-mapping question drafted for Harsha. Both messages ready to send. Still open: roles doc validation + send to Deepak/team. | AITAPA | In-Progress |
| 4 | Deepak's call — still unscheduled (rolled from 08/10, originally 08/07) | Fresh prep + scheduling + attend. | AITAPA | Not started |
| 5 | Weekly sheet hours | Confirm Monday's actual hours (currently TBD) plus Thu 06/08 and Fri 07/08 from last week, still outstanding. | Weekly Status | Not started |
| 6a | Rolled forward — AITAPA | AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation. | AITAPA | Not started |
| 6b | Rolled forward — AITAPC | D001 Production Changes verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook cross-check, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release. | AITAPC | Not started |
| 6c | Rolled forward — daily tracking | Daily status update. | Daily-in | Not started |
| 6d | Rolled forward — unassigned/admin | 2pm KT call, Lukens Matthew email, Task 8 Leela email, both MOMs, BNKC-1642, EPLX KT, Jira Excel compilation. | Others | Not started |

## Progress Log

(One entry appended per check-in, newest last.)

### Day set up (direct from chat)

User pointed out today's page was missing — turned out the date had rolled over to 08/11 while I was still tracking 08/10 as "today." Confirmed via Notion's own timestamps. Created this page, rolled forward all of Monday's tasks since none were confirmed done (no wrap-up was written for 08/10).

### Task 1 status confirmed (direct from chat)

User confirmed: the AITAPA Terraform errors are still not fixed — actively working on it now. Updated Task 1 to In-Progress.

### AITAPA game plan built for Task 3 (direct from chat)

User asked for a forward-looking AITAPA game plan including Jira stories, for Task 3. Built from the architecture review doc — today's Terraform errors are the persona-migration work hitting real blockers, so the plan ties directly to that.

**9 proposed Jira stories, sequenced:**
1. **Resolve Terraform apply blockers — persona RBAC rollout (SCUS)** — Highest, In Progress (= today's Task 1). KV key import, Storage Contributor role check, stale PE state cleanup.
2. **Soft-deleted EUS workspace — purge/recreate** — High, blocks #1 fully resolving. Note: EUS's *second* soft-delete incident — evidence for story 6.
3. **Apply persona RBAC to SCUS sandbox + validate** — High, blocked by 1 & 2. Plan review, sandbox apply, per-persona access test, re-enable CMEK (track explicitly, don't skip).
4. **Confirm Harsha's role-bundle → persona mapping** — Medium, needs Harsha's input not code. UAMI Roles → platform_admin's UAMI (proposed); User Roles → ml_engineer + data_scientist (proposed); group-vs-UAMI role-split design call.
5. **Add outbound network rules to SCUS ML workspace** — Medium, may be partly done — confirm. Full FQDN/PE/ServiceTag rule set already drafted.
6. **Decide EUS's long-term fate** — Medium, decision item (decommission vs. bring to parity).
7. **Fill in test/prod SDLC stubs** — Low, currently non-functional but not urgent.
8. **Code quality cleanup** — Low, opportunistic as files are touched.
9. **Wire up real alerting** — Low, alert scaffolding exists, nothing fires yet.

**Two messages drafted** (clarified: story list goes to the **Scrum Master**, not Harsha — Harsha gets a separate, narrower ask):

> **To Scrum Master — upcoming AITAPA stories for backlog**
>
> Hi [Scrum Master name], here's the list of upcoming AITAPA stories for grooming/sprint planning:
>
> 1. Resolve Terraform apply blockers — persona RBAC rollout (SCUS) — Highest priority, in progress now.
> 2. Soft-deleted EUS workspace — purge/recreate — High priority, blocking #1's full resolution.
> 3. Apply persona RBAC to SCUS sandbox + validate — High priority, blocked by #1/#2.
> 4. Confirm Harsha's role-bundle → persona mapping — Medium, pending input (not blocked on code).
> 5. Add outbound network rules to SCUS ML workspace — Medium, may be partially done, needs confirmation.
> 6. Decide EUS's long-term fate (decommission vs. bring to parity) — Medium, decision item.
> 7. Fill in test/prod SDLC stubs — Low, currently non-functional but not urgent.
> 8. Code quality cleanup (opportunistic) — Low, folded in as files are touched.
> 9. Wire up real alerting — Low, alert scaffolding exists but nothing fires yet.
>
> Happy to walk through priority/sequencing if useful for sprint planning.

> **To Harsha — role-bundle mapping confirmation**
>
> Hi Harsha, working through the persona RBAC rollout for AITAPA and want to confirm the mapping for the role bundles you sent over:
>
> - **"UAMI Roles"** — I'm proposing these apply to platform_admin's UAMI, since it's already the workspace's system identity. Confirm that's right?
> - **"User Roles"** — proposing these apply to ml_engineer and data_scientist (not platform_admin or reader), since they're the personas actively building/running models. Confirm, or let me know if it should be different?
>
> Also — should the same role bundle apply to both a persona's AD group *and* its UAMI, or should those be split into separate lists?
>
> Let me know when you have a minute.

Both drafts ready to send — not yet sent. Still open on Task 3: validate the roles doc and send to Deepak/team.

## Day Summary

*(written at wrap-up)*
