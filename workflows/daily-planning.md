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
  source of truth for re-run/resume logic) as a "Plan" section appended
  below the brain dump content — never a separate page. Add `Planning` to
  that page's `Category` alongside `Brain Dump` once the plan section
  exists. Update that same section at every step that rewrites the local
  file (Step 3 write, each Step 5 check-in, and the Step 6 wrap-up) using
  targeted content updates, not a full-page replace.

## Step 1 — Morning Intake

1. If `output/daily-plan-<YYYY-MM-DD>.md` (today's local date) already
   exists, stop here and go to **Re-run Behavior** below instead of
   re-planning from scratch.
2. Build **Yesterday's Brief** — what carries into today — before touching
   Notion or asking for new tasks:
   - Read yesterday's `output/daily-plan-<yesterday's date>.md`: pull its
     Day Summary (completed vs. not, variance) and its "Rolled to
     tomorrow" list.
   - Cross-check against memory of yesterday's hourly check-ins (Step 5)
     for anything completed or rescoped after the last file write.
   - If yesterday's file is missing, or the completed/rolled-over picture
     is ambiguous (e.g. a task's status was never confirmed in a
     check-in), ask the user directly rather than guessing what carries
     over.
   - Summarize the result as a short brief: completed yesterday (for
     context, not today's list), and rolled-over tasks/subtasks with
     their remaining estimates — these seed today's candidate task list.
3. Create or update today's Notion Brain Dump page with that brief (see
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

1. Send a short `PushNotification`, e.g. "Check-in: what did you finish in
   the last hour? (Task X / Y / none)".
2. Wait for the user's reply on that thread. If the *next* trigger fires
   before a reply arrives, treat it as a missed check-in: note it in the
   Progress Log as "no update received for HH:00-HH:00" and fold that span
   into the new check-in's question instead of losing it.
3. Parse the reply into: tasks/subtasks completed, tasks/subtasks still in
   progress with the user's own remaining-time estimate, and anything
   newly discovered mid-task (scope creep).
4. Update `output/daily-plan-<YYYY-MM-DD>.md` in place, then mirror the
   updated content to today's Notion Document Hub page:
   - Mark completed subtasks/tasks with their actual finish time and
     actual hours. Never rewrite the original estimate — variance is
     reported at wrap-up, not erased.
   - For each unfinished task, refresh its remaining-subtask list and
     remaining-time figure using **the user's own self-reported remaining
     time** — trust their read of where they are rather than
     re-deriving it from the original subtask breakdown.
5. Compute and append a Progress Log entry:
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

## Step 7 — Monthly Hours Log

Still at wrap-up, build the day's compiled hours entry:

1. For each completed task, build one row using its **Actual (h)** from
   the sheet — never the estimate:

   `Date | Jira Number | AppID | Category | Task/Activity Name | ACE Scope | Total Hours`

   - `Jira Number`: from the task if the user gave one; otherwise blank/"N/A"
     (meetings, KT sessions, and other non-ticketed work commonly have none).
   - `AppID` and `Category`: infer from the task description against the
     independent pick-lists in `resources/task-log-reference.md` (these are
     not a fixed pairing — any category can pair with any AppID). Ask the
     user to confirm/correct rather than guessing silently, since AppID
     drives their internal reporting.
   - `ACE Scope`: always blank.
   - `Total Hours`: the task's actual hours.
2. If `workdone/<Mon-YY>.md` (e.g. `workdone/Jun-26.md`) doesn't exist yet
   this month, create it with the header row above. Otherwise append the
   day's rows under the existing table — one running table per month.

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
