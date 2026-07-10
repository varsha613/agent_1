## Day Summary Header

- **Date:** 2026-07-09 (Thursday)
- **Work windows:** 09:00-13:15 (IST, extended 15min for skilling), 17:00-21:30 (IST)
- **Skilling-hour slot:** 12:30-13:15 (45min, shortened by user's choice)
- **Recurring calls today (see resources/recurring-schedule.md):** 17:30-18:30 Elastic SME call, 20:00-20:30 US standup, 20:30-20:45 scrum, 21:00-21:30 daily sync-up with US lead
- **Total available:** ~8.75h (5.75h task-work + 0.75h skilling + 2.25h recurring calls)
- **Total estimated task-work:** 5.25h (vs 5.75h available; Task 2 is contingent; includes 30min already done pre-window on Elastic prep)
- **Check-in trigger ids:** trig_012ZoUZL2uL7XrWVSpF5cr7r (10:00), trig_0127stm1yJ4iJRC3o2czXdK4 (11:30), trig_011Qf2Ki8Hmjjs1PwYD1qWpT (12:30), trig_01FCjku5mUuNWiZr1szwe5Z3 (19:00), trig_01MdyUpi2iXiusGZUdXQUnMJ (21:00 wrap-up) — all IST. 18:30/19:30/21:30 triggers deleted and replaced by user request (schedule shifted 30min earlier); ~6:19pm check-in run ad hoc instead of waiting for 18:30.
- **Status:** planned

## Tasks

| # | Task | Priority/Deadline | Est. (h) | Subtasks (est.) | Status | Actual (h) |
|---|------|--------------------|----------|------------------|--------|------------|
| 1 | Update AITAPA module (Harsha's path) + apply CMEK combined, deploy | Fri ETA | 1.25 | | blocked — version constraint error (v1.2.0-beta.1 unavailable, newest is 1.1.0), switching pin and re-running | |
| 2 | Resolve outbound rule errors (contingent — post-deploy) | Fri ETA | 1.0 | | not started (confirmed) | |
| 3 | ML Registry subscription — send out status message | - | 0.25 | | completed — expanded into full architecture analysis (see notes) | ~0.75 |
| 4 | Prisma: raise at least 4 more tickets, add to Jira, forward to Deepak | - | 0.75 | | not started (confirmed) | |
| 5 | Elastic prep: gather info on how Sudhir ran the DEV validation without bringing the cluster down, write up KT notes/documentation and send out, upskill on what wasn't understood from yesterday's KT | Fri (AIADB) | 1.5 (+0.5 already done pre-window) | | in progress — expanded well beyond "prep" into real VDB/LLDS architecture work (see notes) | ~1.5 |

**Task 3 detail (ML Registry):** surfaced a real blocker — creating an ML Registry resource requires Azure-managed resources not permitted under current Wells Fargo policy in the existing subscription. Resolution path: a separate Azure subscription with a policy exemption must be provisioned. This changes the target architecture (two subscriptions instead of one) and needs formal governance approval before proceeding. Deepak will reach out to the Potsi team; discussed further in tomorrow's internal follow-up call. Three supporting docs created in Notion.

**Task 5 detail (Elastic, done ahead of the 17:00 slot):** reviewed architecture across VDB dev/UAT/Prod and LLDS dev/UAT (VDB UAT is treated like Production — holds real non-synthetic data, needs prior notice for any work there). LLDS UAT already has the S3 plugin installed but its snapshot repo is currently failing ("could not determine repository generation from root blobs" — needs troubleshooting). VDB has no snapshot/restore policy yet — starting from scratch in dev. **Blockers:** no bucket-creation permissions (read/write only) — working with Tanya to either get a dedicated bucket or temporary sign-off to use the existing AMLP QA bucket for the dev proof-of-concept; 4 HPOS entitlements raised and pending approval (following up with Sanjeev). Also requested the production team split their bundled VDB+LLDS cutover change ticket to do LLDS first (not yet agreed). Plan: install S3 plugin in VDB dev (if needed) → keystore creds + JVM cert bypass → restart cluster → create/verify S3 snapshot repo → daily snapshot policy (1:30am, 30-day retention) → validate over several cycles → replicate to UAT. Target: dev setup complete by Friday, but full validation trails since it needs multiple successful cycles. Email drafted to Sanjeev/Kalai summarizing all of this.

**Context — Sudhir's 6:27am email to Sanjeev:** HPOS snapshot onboarding/validation fully completed and validated in DEV (repo registration, connectivity, snapshot creation, storage validation, restore validation, recovery verification) — documented in Confluence. Next: same workflow in UAT, targeting completion today, with Friday held as contingency for any UAT-specific issues.

**Heads up for tomorrow (not actionable today):** TFE will be down Fri 2026-07-10 21:00 ET for 4-6h (server updates) — affects Task 1/2 (Terraform-dependent) if they slip to Friday evening ET.

**Resolved:** status email sent today, updated with Sudhir's DEV-validation progress (was the open item from yesterday's draft to Kiran, Kalai, Keshvam re: VDB-LLDS UAT outage).

**Deferred (not today):** compile all Jira tickets worked on since Feb 2026 into Excel — requires a Jira data export I don't have access to pull myself; today stays focused on the Friday deadlines.

**Cleared:** inbox — no other flagged items today.

**Stretch (buffer only, not urgent):** AITAPA documentation.

(The skilling hour and recurring calls appear in the Timeline below but are
not rows here and are excluded from % done / % left math. % math uses the
5.75h task-work pool as the denominator.)

## Timeline (resequenced at 10:05am — Task 3/5 ran long, ate window 1's morning budget)

- 09:00-10:05 — Task 3 (expanded into architecture analysis) + Task 5 (Elastic, ahead of schedule)
- 10:05-11:20 — Task 1: Module + CMEK update, deploy (highest priority — Friday ETA)
- 11:20-11:50 — Task 2: Outbound rule errors (partial, 30 of 60min — contingent)
- 11:50-12:30 — Task 4: Prisma tickets (partial, 40 of 45min)
- 12:30-13:15 — Skilling (45min)
- *(Remaining ~35min of Task 2/4 will need to squeeze into tonight's buffer slots — tight, flagging now.)*
- 13:15-17:00 — (off-window)
- 17:00-17:30 — Task 5: Elastic prep (start)
- 17:30-18:30 — Elastic SME call
- 18:30-19:30 — Task 5: Elastic prep (finish)
- 19:30-20:00 — Buffer
- 20:00-20:30 — US team standup
- 20:30-20:45 — Daily scrum
- 20:45-21:00 — Buffer
- 21:00-21:30 — Daily sync-up (US team lead)

## Progress Log

(One entry appended per check-in, newest last.)

### 10:00 check-in

- Completed: Task 3 (ML Registry) — expanded into full architecture analysis, surfacing a major blocker (separate Azure subscription + policy exemption needed). 3 docs created.
- In progress, ahead of schedule: Task 5 (Elastic) — real VDB/LLDS architecture review and implementation planning done well beyond the planned "prep only" scope; email drafted to Sanjeev/Kalai with blockers (bucket-creation permissions, HPOS entitlements) and a Friday dev-setup target.
- Not confirmed: Task 1 (module + CMEK, deploy), Task 2 (outbound rule), Task 4 (Prisma tickets) — no update given yet, asked directly.
- Notes: given how much ground Task 3/5 covered already, today's timeline will likely need resequencing once Task 1/2/4 status comes in.

### 11:30 check-in

- Found directly in Notion (no chat reply yet): a Terraform module block snippet — `source = "https://tfe-nonprod.wellsfargo.net/TFE-PSCDE-shared/wf-machine-learning/azurerm/<submodule_name>"`, `version = "v1.2.0-beta.1"` — this is Harsha's new module path being wired into Task 1's config, pinned to a beta version.
- Not yet confirmed: whether Task 1 is deployed/validated, or still mid-edit. Task 2 and Task 4 status also still unconfirmed. Asked directly.

### 12:30 check-in

- No new updates found in Notion since 11:30. Still not confirmed: Task 1 (deploy status), Task 2 (outbound rule), Task 4 (Prisma tickets). Asked directly.
- Skilling (45min) starts now. Next check-in is 18:30 IST, after the Elastic SME call.

### 6:19pm check-in (run ad hoc, replacing the scheduled 18:30 one; remaining check-ins shifted 30min earlier to 19:00 and 21:00 wrap-up)

- **Unplanned call:** ACE India team, 1h15m (1.25h) — new team responsibilities discussed; shift time moving to 2pm-11pm (Kalai pursuing a shift allowance); need a follow-up call with Kalai to document hours/tasks for bandwidth; new "EPLX" skill/learning category added, with ~4h of KT sessions to go through. **Unplanned-call tally so far today: 1 call, 1.25h.**
- **Task 1:** hit a Terraform error — `Unresolvable module version constraint`, the pinned `v1.2.0-beta.1` doesn't exist, newest available is `1.1.0`. Switching the version pin and re-running. Status: blocked (in progress on fix).
- Not yet confirmed: Task 1 outcome after the version fix, Task 2, Task 4, and whether the 2pm-11pm shift starts today or later. Asked directly.

### 19:00 check-in

- No new updates found in Notion since 6:19pm. Still not confirmed: Task 1 outcome (1.1.0 fix), Task 2, Task 4, shift start date. Asked directly.
- Standup/scrum/sync-up follow at 20:00-21:00. Next check-in is the 21:00 wrap-up.

## Day Summary (written at wrap-up)

- **Completed:** Task 3 (ML Registry — expanded into full architecture analysis, blocker surfaced), ~0.75h.
- **In progress, carried over:** Task 5 (Elastic) — substantial VDB/LLDS architecture work, status email, and a KT-summary email drafted; ~1.5h+ logged, continues Friday.
- **Task 1:** confirmed (via user, 10 Jul ~10:15pm) still blocked on the Terraform version-constraint error at day's end — never resolved same-day. Continues tonight (Friday) as the top priority.
- **Task 2, Task 4:** status was never confirmed despite check-ins at 10:00, 11:30, 12:30, 6:19pm, and 7pm — presumed not completed. Rolled to Friday.
- **Unplanned:** ACE India team call, 1h15m (1.25h) — shift-time change to 2pm-11pm proposed (start date unconfirmed), new "EPLX" skill category with ~4h of KT sessions pending.
- **Total actual hours confidently logged:** ~2.25h task-work (Task 3 + partial Task 5) + 1.25h unplanned call = ~3.5h. Likely an undercount given the day closed without full confirmation.
- **Rolled to Friday (today, the deadline day):** Task 1 (fix module version issue + test — in progress now), Task 2, Task 4, Elastic UAT execution, documentation of recent work, AITAPA documentation (stretch, still untouched).
- **Final status:** incomplete close-out — several check-ins went unanswered and the wrap-up itself landed roughly 25h late (user returned late Friday night). Continuing directly into Friday's session rather than reconstructing exact same-day figures.
