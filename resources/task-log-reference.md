# Task Log Reference Lists

Fixed lookup lists and column rules used by `workflows/daily-planning.md`
Step 7 when filling each task's row in `workdone/<Mon-YY>.md` — this file
doubles as both the monthly hours log and the daily team status Excel
input, per the user's tracker template.

## Columns (in order)

| Column | Rule |
|--------|------|
| Date | MM/DD/YYYY |
| JIRA No. with Link | The task's Jira ticket number, hyperlinked to its URL (markdown `[TICKET-123](url)`). Only known if the user gave it when the task was set up (see below) — otherwise `NA`. Always `NA` for `Meetings` or `KT sessions` category rows. |
| AppID | See list below. Independent pick from Category — not a fixed pairing. |
| Category | See list below. |
| Task/Activity Name | Brief summary of the task/activity performed. |
| ACE Scope | Always left blank in every row (per user instruction — revisit if they say otherwise). |
| Total Hours | Actual hours spent, never the estimate. |
| Due Date (If any) | MM/DD/YYYY, from any deadline noted for the task (e.g. a Friday ETA). `NA` for `Meetings` or `KT sessions`. |
| Status | `Not Started` / `In-Progress` / `Blocker` / `Completed` — the task's state as of wrap-up. |
| Blockers | Description of any blocker, the dependent team/person, and relevant Jira/email references. `NA` for `Meetings` or `KT sessions`, or if there was no blocker. |
| Remarks/Comments | Any additional clarifying note on status/progress (e.g. "will attach ticket once I get dashboard access"). |

**Getting the Jira number**: ask the user for a task's Jira ticket number
when the task is first set up (Step 1/Step 2 — brain dump intake or
estimation), not retroactively at wrap-up. If they don't have one yet,
leave it `NA` for that day and ask again next time the task reappears.

## Category

- Regular support
- New Initiatives
- Migration Activities
- Meetings
- Automation
- Production Calls
- Production Preparedness
- Info for Management
- Mandatory Trainings
- Patching Activities
- Debugging Sessions
- Adhoc Request
- KT sessions
- Tachyon Infra Activities
- Miscellaneous

## Status

- Not Started
- In-Progress
- Blocker
- Completed

## AppID

- AITACA
- AITACG
- AITEUC
- AIDLP
- AIRBT
- AITAPA
- AITAPC
- AIMLP
- MLOPS
- AIADB
- AITACO
- Others

## ACE Scope

Always left blank in every row (per user instruction, 2026-07-09).
