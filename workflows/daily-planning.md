# Daily Planning Workflow

Triggered when the user gives a morning brain dump, says "plan my day," or
replies to an hourly check-in notification. Produces a daily task sheet with
a realistic timeline, roughly-hourly progress check-ins that survive the
terminal being closed, and a compiled monthly hours log for reporting.

Related files: `resources/daily-plan-template.md`,
`resources/task-time-estimation-heuristics.md`, `resources/task-log-reference.md`,
`resources/recurring-schedule.md`.

At Step 1/Step 3, check `resources/recurring-schedule.md` for standing
calls that fall inside today's work windows and block that time out
before sequencing tasks — don't ask the user to re-state these daily.
Flag it to the user if today looks like it might deviate from the
standing pattern, rather than silently assuming it holds.

## Notion Integration

One page per day holds everything. The **Document Hub** data source
(`collection://3917a5e7-c4ee-80ef-93a1-000b3292f6c8`) holds daily pages with
a `Doc name` title property (format `DD Mon YY`, e.g. `07 Jul 26`) and a
`Category` multi-select.

- **I create today's page, not the user.** At Step 1, before asking
  anything else, build **Yesterday's Brief** (see Step 1.2) and create a
  page in Document Hub with `Doc name` = today's date and `Category`
  containing `Brain Dump`, whose body opens with that brief followed by a
  "Today's Brain Dump" section for the user to fill in. Skip creation if a
  page already matching today's date exists (e.g. re-running Step 1 later
  the same day, or the plan section already added) — update it in place
  instead of duplicating the page.
- Tell the user the page is ready and wait for them to add today's new
  tasks directly in Notion. Don't move to Step 2 until they confirm
  they're done adding tasks.
- **Reading**: once the user confirms, fetch today's page, and parse tasks
  from the Yesterday's Brief section plus whatever the user added, the
  same way a chat brain dump would be parsed.
- **Work windows and skilling-hour placement still come from chat**, asked
  directly each day per Step 1.3 below — they are not read from Notion.
- **Writing**: the day's plan is mirrored into the *same* page (in addition
  to the local `output/daily-plan-<YYYY-MM-DD>.md` file, which remains the
  source of truth for re-run/resume logic) as a "Plan" section — never a
  separate page. Add `Planning` to that page's `Category` alongside
  `Brain Dump` once the plan section exists. Update that same section at
  every step that rewrites the local file (Step 3 write, each Step 5
  check-in, and the Step 6 wrap-up) using targeted content updates, not a
  full-page replace.
- **"Today's Brain Dump" always stays the last section on the page.** The
  user adds to it throughout the day, so don't let Plan/Progress
  Log/Day Summary content get appended after it. When writing any of
  those sections for the first time, insert them immediately *before*
  the "## Today's Brain Dump" heading (anchor on that heading in the
  search-and-replace), not at the end of the page.
- **Completed checkbox**: Document Hub has a `Completed` checkbox property.
  When Step 1 runs for a new day, check yesterday's Document Hub page as
  `Completed` (it's done being actively worked, wrap-up already ran)
  before or while creating today's page — this is what lets the table show,
  at a glance, which days are closed out. Today's own page stays unchecked
  until the *next* day's Step 1 runs.
- **Timeline lives inside the Tasks table, not a separate section**
  (changed 2026-07-14). Add a `Time` column (e.g. `1:30-2:45pm`) alongside
  `#`/`Task`/`Est. (h)`/`Status` in the Tasks table, in **both** the local
  `output/daily-plan-<date>.md` file and the Notion mirror — do not write
  a standalone "### Timeline" section in either place anymore.
- **Times are always 12-hour with am/pm** (changed 2026-07-14), e.g.
  `1:30pm`, `9:00am` — not 24-hour/military time — everywhere a time is
  written: the Time column, work windows, recurring-call times, check-in
  references, etc.
- **Check-in updates go directly in the Tasks table** (changed
  2026-07-14). Add a `Check-in Update` column to the Tasks table (both
  local file and Notion mirror) so the user can type their progress
  against a specific task row directly, instead of only replying in chat
  or writing in the Brain Dump section. At Step 5, when checking Notion
  first, read this column for anything new since the last check-in the
  same way the Brain Dump section is checked — it's another place a
  direct update can show up. When a check-in's update is parsed and
  folded into the Progress Log / Status / Actual (h) fields, clear or
  summarize the cell rather than leaving stale text sitting there for
  the next check-in to re-read.

## Step 1 — Morning Intake

1. If `output/daily-plan-<YYYY-MM-DD>.md` (today's local date) already
   exists, stop here and go to **Re-run Behavior** below instead of
   re-planning from scratch.
2. Build **Yesterday's Brief** — what carries into today — before touching
   Notion or asking for new tasks:
   - "Yesterday" means the most recent prior **work day** per
     `resources/recurring-schedule.md` (Mon-Fri), not literal
     calendar-yesterday — on a Monday this is the prior Friday, skipping
     the weekend. If the session picking this up is itself several days
     late (e.g. resuming Monday after a Friday-night session that never
     got wrapped up), close out and mirror that stale day first (mark it
     `wrapped-up` in the local file and `Completed` in Notion) before
     building today's brief from it.
   - Read that day's `output/daily-plan-<date>.md`: pull its Day Summary
     (completed vs. not, variance) and its "Rolled to tomorrow" list.
   - Cross-check against memory of yesterday's hourly check-ins (Step 5)
     for anything completed or rescoped after the last file write.
   - If yesterday's file is missing, or the completed/rolled-over picture
     is ambiguous (e.g. a task's status was never confirmed in a
     check-in), ask the user directly rather than guessing what carries
     over.
   - Summarize the result as a short brief: completed yesterday (for
     context, not today's list), and rolled-over tasks/subtasks with
     their remaining estimates — these seed today's candidate task list.
3. Mark yesterday's Document Hub page as `Completed` (checkbox), then
   create or update today's Notion Brain Dump page with that brief (see
   **Notion Integration** above), tell the user it's ready, and wait for
   them to add today's new tasks in Notion before continuing.
4. Once the user confirms, fetch today's Brain Dump page and extract:
   - Discrete tasks (split run-on descriptions into separate items),
     combining the rolled-over tasks from Yesterday's Brief with whatever
     new tasks the user added.
   - Any deadlines, priorities, or explicit "must finish today" items.
5. Ask the user directly in chat for:
   - Today's **work windows** — one or more start–end blocks. The user's
     schedule varies day to day: some days are one flexible block, office
     days (~3x/week) are chunked around lunch/commute/gym (e.g.
     `07:00-13:00` then `17:30-20:30`). Never assume a default — ask
     explicitly if not stated.
   - Where the **1h skilling block** falls within those windows.
6. If work windows or the skilling-hour placement are missing, ask before
   proceeding. Task-work pool = total window time - 1h skilling = should
   sum to 8h; flag it if the stated windows don't add up to ~9h total.

## Step 2 — Time Estimation

1. Estimate each task's duration using
   `resources/task-time-estimation-heuristics.md`, plus domain context from
   `claude.md` (Terraform Enterprise, Vault, RBAC/Landing Zone, Private
   Endpoint/DNS, ELK, Prisma remediation, Azure/GCP work).
2. Break anything estimated at more than 1h into 2-4 subtasks with their
   own estimates — needed later for subtask-level progress tracking, so
   don't skip this even if the brain dump described it in one line.
3. Show the estimate table to the user. Wait for confirmation or
   corrections before locking anything in — do not proceed to sequencing
   until the user confirms.

## Step 3 — Sequencing

1. Lay tasks across the stated work windows in priority/deadline order;
   default to the order given if no explicit priority. Place the skilling
   block at the stated placement — never assume it's first, last, or
   mid-day.
2. If total estimated task-work exceeds 8h, stop and ask the user which
   task(s) to trim, defer, or shrink rather than silently overcommitting
   the day.
3. Write `output/daily-plan-<YYYY-MM-DD>.md` using the structure in
   `resources/daily-plan-template.md`, then mirror it to today's Notion
   Document Hub page per **Notion Integration** above.

## Step 4 — Set Up Today's Hourly Check-Ins

Use the `/schedule` skill (backed by the `RemoteTrigger` tool), not
`CronCreate` — check-ins must survive the terminal closing, and `CronCreate`
jobs are session-only and die when the session exits.

1. Compute check-in timestamps: roughly one per hour of task-work time,
   inside each active work window only (skip window gaps like
   lunch/commute/gym, and skip the skilling hour itself). The final
   timestamp, at the end of the last window, is the "wrap-up" firing
   rather than a normal check-in.
2. Create the routine via `RemoteTrigger action=create` with a cron
   pinned to **today's exact date** (day-of-month + month fields) so it
   structurally cannot fire on a future day — `RemoteTrigger` has no
   delete action, so this pinning is what scopes it to today, not cleanup.
3. The routine's prompt must be self-contained, since each firing is an
   independent agent invocation:
   - Re-read today's `output/daily-plan-<YYYY-MM-DD>.md` for current state.
   - If the fire time is at/after the end of the last work window, run
     **Step 6 (End-of-Day Wrap-Up)** instead of a regular check-in.
   - Otherwise run **Step 5 (Hourly Check-In)**.
4. After creating the trigger, tell the user plainly: each check-in is a
   push notification plus a resumable prompt, not a live blocking question
   in one open terminal — replying is what continues that specific
   check-in's thread, which is a different experience than a synchronous
   back-and-forth in a running session.
5. Record the returned `trigger_id` in the sheet's Day Summary header.
6. Sanity-check timezone handling: on first real use, confirm via
   `RemoteTrigger action=get` (or the summary line returned by
   `create`/`update`) what time the trigger reports before trusting it for
   a full day of check-ins.

## Step 5 — Hourly Check-In (what fires each hour)

1. **Before sending the push notification, fetch today's Notion page.**
   The user frequently logs progress directly in Notion (Brain Dump
   section or elsewhere on the page) instead of, or ahead of, replying
   in chat. If there's new content since the last check-in, treat it as
   this check-in's update — incorporate it into the Progress Log the
   same as a chat reply — rather than waiting on a reply that may never
   come.
2. Send a short `PushNotification` regardless of what Notion showed, e.g.
   "Check-in: what did you finish in the last hour? (Task X / Y / none)"
   — or, if Notion already had an update, something that confirms what
   was found and only asks about what's still missing.
3. Wait for the user's reply on that thread. If the *next* trigger fires
   before a reply arrives (and nothing new turned up in Notion either),
   treat it as a missed check-in: note it in the Progress Log as "no
   update received for HH:00-HH:00" and fold that span into the new
   check-in's question instead of losing it.
4. Parse whatever update was found (Notion and/or chat reply) into:
   tasks/subtasks completed, tasks/subtasks still in progress with a
   remaining-time estimate, and anything newly discovered mid-task
   (scope creep).
   - **Whenever an unplanned/unscheduled call is mentioned** (not one of
     today's already-scheduled recurring calls), always ask how long it
     lasted if the duration wasn't given — don't estimate or skip this.
     Track a running per-day tally of unplanned-call count and total
     call-hours; this feeds the `Daily Status` output at wrap-up (Step 7)
     as its own line, separate from task rows.
5. Update `output/daily-plan-<YYYY-MM-DD>.md` in place, then mirror the
   updated content to today's Notion Document Hub page:
   - Mark completed subtasks/tasks with their actual finish time and
     actual hours. Never rewrite the original estimate — variance is
     reported at wrap-up, not erased.
   - For each unfinished task, refresh its remaining-subtask list and
     remaining-time figure using **the user's own self-reported remaining
     time** — trust their read of where they are rather than
     re-deriving it from the original subtask breakdown.
6. Compute and append a Progress Log entry:
   - `% day done` = (hours of fully-completed tasks + completed-subtask
     hours within partially-done tasks) / 8 x 100. `% day left` = 100 minus
     that. (The skilling hour is excluded — it's fixed overhead, not "progress".)
   - `Remaining subtasks`: a flat list grouped by parent task, each with
     its (possibly revised) estimate.
   - `Remaining estimated time` = sum of those revised subtask estimates.
   - `Remaining time in day` = sum of what's left in today's *still-upcoming
     work windows* — not wall-clock time, so gaps between windows
     (lunch/commute/gym) don't count against the user.
   - Status flag, comparing remaining-estimated vs remaining-in-day:
     - within ±15 min → **ON TRACK**
     - 15-45 min over → **BEHIND - minor** (mention it, no action needed)
     - more than 45 min over → **BEHIND - flag**, and proactively suggest a
       concrete trim (defer a specific low-priority task, shrink a
       subtask, or extend the day) rather than just reporting the number
     - well under remaining-in-day → **AHEAD**, note the buffer and
       optionally suggest pulling a task forward
6. Only send a second push notification (beyond the routine hourly one) if
   the flag is **BEHIND - flag** — don't over-notify for routine updates.

## Step 6 — End-of-Day Wrap-Up

Fires at the final scheduled timestamp instead of a normal check-in.

1. Compute the final day summary: tasks/subtasks completed vs. not, total
   actual vs. total estimated hours, overall variance, and final
   on-track/behind/ahead status.
2. Append a "Day Summary" section to the bottom of today's plan file (per
   the template) — this file is the day's permanent record, nothing is
   deleted. Mirror the final content to today's Notion Document Hub page.
3. List any unfinished tasks/subtasks under "Rolled to tomorrow." Do not
   auto-create tomorrow's file — tomorrow's Step 1 intake reads this list
   and offers it before the new brain dump.
4. Best-effort: try `RemoteTrigger action=update` to deactivate today's
   trigger as housekeeping. Not load-bearing — the date-pinned cron
   already guarantees it can't fire again tomorrow regardless of whether
   this succeeds.

## Step 7 — Monthly Hours Log / Team Status Excel Input

This one file (`workdone/<Mon-YY>.md`) serves double duty: it's both the
monthly hours log and the daily input for the user's team status Excel.
Column rules and pick-lists live in `resources/task-log-reference.md` —
read that file for the full spec. Still at wrap-up, build the day's
compiled entry:

1. For each task touched today (not just completed ones — include
   `In-Progress` and `Blocker` rows too, since the team status sheet
   tracks all of those), build one row:

   `Date | JIRA No. with Link | AppID | Category | Task/Activity Name | ACE Scope | Total Hours | Due Date (If any) | Status | Blockers | Remarks/Comments`

   - `Date`: MM/DD/YYYY.
   - `JIRA No. with Link`: only if the user gave a ticket number when the
     task was set up (see Step 1a below) — hyperlinked as
     `[TICKET-123](url)`. Otherwise `NA`. Always `NA` for `Meetings` or
     `KT sessions` rows.
   - `AppID` and `Category`: infer from the task description against the
     independent pick-lists in `resources/task-log-reference.md` (not a
     fixed pairing). Ask the user to confirm/correct rather than guessing
     silently, since AppID drives their internal reporting.
   - `ACE Scope`: always blank (per user instruction — revisit if they
     say otherwise).
   - `Total Hours`: the task's actual hours, never the estimate.
   - `Due Date (If any)`: MM/DD/YYYY from any deadline noted for the task
     (e.g. a Friday ETA). `NA` for `Meetings`/`KT sessions`.
   - `Status`: `Not Started` / `In-Progress` / `Blocker` / `Completed`.
   - `Blockers`: description + dependent team/person + relevant
     Jira/email references, or `NA` if none (always `NA` for
     `Meetings`/`KT sessions`).
   - `Remarks/Comments`: any clarifying note worth surfacing to the team.
2. If `workdone/<Mon-YY>.md` (e.g. `workdone/Jun-26.md`) doesn't exist yet
   this month, create it with the header row above. Otherwise append the
   day's rows under the existing table — one running table per month.
3. Mirror the same rows into today's Notion page as a "## Daily Status
   (Team Excel Input)" table, inserted right after the Day Summary
   section (still before "Today's Brain Dump" per the ordering rule
   above). Use the enhanced-markdown `<table>` format for the columns.
4. Add an "Unplanned calls today" summary line right after the table:
   count of unplanned/unscheduled calls and their total hours (from the
   per-day tally kept in Step 5) — e.g. "3 unplanned calls, 2.25h total."
   Don't count today's already-scheduled recurring calls in this tally.

**Step 1a — capture Jira numbers at task setup, not at wrap-up.** When a
task is first added (Step 1 brain dump intake, or Step 2 estimation), ask
the user if it already has a Jira ticket number. Skip this for
`Meetings`/`KT sessions`-flavored tasks. If they don't have one yet,
record `NA` for now — don't chase it down retroactively at wrap-up.

## Re-run Behavior (today's file already exists)

If `output/daily-plan-<YYYY-MM-DD>.md` already exists when Step 1 runs, ask
the user explicitly which of these they want — do not guess:

- **Amend** — add new tasks to today's existing plan. Re-estimate only the
  new tasks, recompute the remaining-time pool from the *current* time
  (not the original 8h), append them under an "Added mid-day" marker, and
  re-derive the check-in schedule (Step 4) from now forward — update the
  existing trigger's cron if `RemoteTrigger action=update` supports it,
  otherwise create a new trigger for the remainder of the day (the old one
  is already harmless since it's date-pinned).
- **Replan** — full redo. Archive the existing file to
  `output/daily-plan-<YYYY-MM-DD>.v1.md` (increment the suffix if a v1
  already exists), then run Steps 1-4 fresh.
- **Resume** — no changes to the plan; just re-read the file and report
  current status (useful after reopening a closed terminal).

## Folder setup

Create `workflows/`, `output/`, `resources/`, `workdone/` on first run if
any are missing — they should already exist after this workflow is set up,
but a fresh clone of this workspace won't have `output/` or `workdone/`
populated until the first real day runs.
