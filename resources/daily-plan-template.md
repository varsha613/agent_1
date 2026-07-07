# Daily Plan Template

Used by `workflows/daily-planning.md` when writing
`output/daily-plan-<YYYY-MM-DD>.md`. Copy this structure for every new day.

---

## Day Summary Header

- **Date:** YYYY-MM-DD
- **Work windows:** HH:MM-HH:MM (, HH:MM-HH:MM if a second window)
- **Skilling-hour slot:** HH:MM-HH:MM
- **Total available:** 9h (8h task-work + 1h skilling)
- **Total estimated task-work:** X.Xh (vs 8h available — flag if over)
- **Check-in trigger id:** <RemoteTrigger id, filled in after check-ins are scheduled>
- **Status:** planned / in-progress / wrapped-up

## Tasks

| # | Task | Priority/Deadline | Est. (h) | Subtasks (est.) | Status | Actual (h) |
|---|------|--------------------|----------|------------------|--------|------------|
| 1 | ... | ... | 1.5 | a) ... (0.5)  b) ... (1.0) | not started | |

(The skilling hour appears in the Timeline below but is not a row here and
is excluded from all % done / % left math — it's fixed overhead, not "progress".)

## Timeline

- HH:MM-HH:MM — Task 1
- HH:MM-HH:MM — Skilling
- HH:MM-HH:MM — Task 2
- ...

## Progress Log

(One entry appended per check-in, newest last.)

### HH:MM check-in

- Completed: ...
- Still in progress: Task #, remaining subtasks: [...], revised remaining est: X.Xh
- % day done: XX%  |  % day left: XX%
- Remaining estimated time: X.Xh  |  Remaining time in day: X.Xh
- Status: ON TRACK / BEHIND (minor) / BEHIND (flag) / AHEAD  [+ gap if a check-in was missed]
- Notes: ...

## Day Summary (written at wrap-up)

- Completed: N/M tasks, X.Xh actual vs Y.Yh estimated (variance: ±Zh)
- Rolled to tomorrow: [task/subtask list]
- Final status: ...
