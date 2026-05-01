---
name: task-log-update
description: |
  Use when the user asks to log work, record what was done, or save task
  progress. Creates a structured markdown task log in `agent-logs/` with
  validation, waivers, and a final gates summary.
---

# Record a task log entry

Create a compact markdown log in `agent-logs/` when meaningful work is completed.

## Filename

- `YYYY-MM-DD-short-task-name.md`

## Required fields

- Task title
- Date
- Scope
- Change classes
- Files changed
- Why
- Validation
- Waivers
- Risks/follow-up
- Memory updates
- Gates summary

## Template

```/dev/null/template.md#L1-13
# Task Title

- Date:
- Scope:
- Change classes:
- Files changed:
- Why:
- Validation:
- Waivers:
- Risks / follow-up:
- Memory updates:
- Gates summary:
```

## Procedure

1. Create a new log file in `agent-logs/` using the filename format above.
2. Fill all required fields with concise, task-specific content.
3. Redact sensitive values.
4. Verify all required fields are present before finishing.

## Rules

- Skip logs for trivial read-only exploration.
- Keep `Validation`, `Waivers`, and `Gates summary` aligned.
