# Task Time Estimation Heuristics

Starting-point buckets for estimating task duration, tailored to this user's
actual work domain. Always show the estimate to the user before locking it
in — these are a starting point, not a final answer.

- **Terraform Enterprise change**: 0.5-1h for a small module/var edit and
  plan review; 1.5-3h for new workspace/module wiring or a multi-env rollout.
- **HashiCorp Vault credential/policy work**: 0.5-1h for a policy tweak or
  secret rotation; 1.5-2.5h for a new auth method/role/lease flow.
- **RBAC / Landing Zone automation**: 1-2h for a role assignment or policy
  change; 2-4h for a new landing zone pattern or subscription-wide rollout.
- **Private Endpoint & DNS**: 0.5-1.5h for a single endpoint + DNS record;
  2-3h for multi-service/multi-vnet peering work.
- **ELK onboarding**: 1-2h per log source/index pattern; 3-4h for a new
  pipeline or dashboard build.
- **Prisma Cloud remediation (GCP)**: 0.25-0.5h per low/medium finding;
  1-2h per high/critical finding needing investigation + fix + verify.
  Scale by finding count if the brain dump lists several.
- **Recurring/BAU tickets, standups, status updates**: 0.25-0.5h.
- **Meetings**: use the stated/calendar duration directly, don't estimate.
- **Skilling**: exactly the day's stated skilling-hour duration (1h) — fixed
  overhead, not separately estimated.
- **Ambiguous "figure out X" / investigation tasks**: default to a 1h block,
  flagged as low-confidence, and ask the user to confirm scope.
- **Unknown-scope buffer**: when a task's size truly can't be inferred from
  its description, default to 1h and say explicitly that the estimate is
  low-confidence rather than silently guessing a number.
