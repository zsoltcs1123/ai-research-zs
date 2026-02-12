# Create Task — Field Rules

Rules for populating custom fields when creating tasks.

## story-points

- Use Fibonacci scale: 1, 2, 3, 5, 8, 13
- Infer from task complexity and subtask count
- Do not assign 0 or values above 13 — split the task instead
- Do not ask the user; always infer

## workstream

- Valid values: `platform`, `idx`, `energyapp`, `gateway`
- Infer from task context (target app, affected area)
- If ambiguous, ask the user — do not guess

## type

- Default to `task` for standard work items
- Use `feature` only for large, user-facing features
- Use `bug` only for defect reports
- Do not invent other types

## labels

- Value is a string array; apply one or more from the table below
- Infer from task content — do not ask the user

| Label      | Description                   |
| ---------- | ----------------------------- |
| `backend`  | .NET backend work             |
| `frontend` | Angular frontend work         |
| `infra`    | Infrastructure, Docker, CI/CD |
| `design`   | UX/UI design tasks            |
| `spec`     | Specification, requirements   |
| `docs`     | Documentation                 |
| `spike`    | Investigation, POC, research  |
| `bug`      | Defects                       |

- Do not apply labels that don't appear in this table
- A task can have multiple labels (e.g. `["backend", "infra"]`)
