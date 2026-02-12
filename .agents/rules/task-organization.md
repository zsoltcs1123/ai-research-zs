# Task Organization

Tasks are grouped by phase.

## Storage

- Phase folders: `docs/phases/phase-{XX}/`
- Task state: `docs/phases/phase-{XX}/phase-{XX}-tasks.json`
- Phase description: `docs/phases/phase-{XX}/phase-{XX}.md`

## Task ID Format

- `p{XX}-task-{YYY}` (e.g., `p01-task-001`)
- `XX` = zero-padded phase number
- `YYY` = zero-padded sequential number within the phase

## ID Generation

- Extract phase number `XX` from the phase
- Scan `phase-{XX}-tasks.json` for the highest existing task number
- Increment by one to get the next ID

## ID Resolution

- Parse phase number from the `pXX` prefix of the task ID
- Find the phase folder at `docs/phases/phase-{XX}/`
- Read/write `phase-{XX}-tasks.json` for that phase

## Creating Tasks

- Phase must be provided by user or inferred from context
- If phase is missing and cannot be inferred, ask user
- Append new task to `phase-{XX}-tasks.json`
- Append entry to `phase-{XX}.md` if not already present (skip when tasks originate from a work breakdown that pre-populates the phase file)

## Grouping

- Each phase has its own `tasks.json` and description file
- If a phase folder doesn't exist, create it
- If `phase-{XX}-tasks.json` doesn't exist, create with empty array `[]`
