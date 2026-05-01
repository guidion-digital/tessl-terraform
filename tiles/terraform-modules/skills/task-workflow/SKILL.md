---
name: task-workflow
description: |
  Use when the user asks you to implement a feature, fix a bug, or complete a
  repository task end-to-end (from scoping through code changes, validation,
  and final gate summary).
---

# Execute the default task workflow

## Procedure

1. Classify change type: `docs-only`, `terraform-module`, `example-terraform`, `ci-workflow`, `mixed`.
2. Read only relevant files. Start with tile docs indexes:
   - `docs/repo-indexes/repo-root.md`
   - `docs/repo-indexes/modules.md`
   - `docs/repo-indexes/examples.md`
   - `docs/repo-indexes/github.md`
3. Choose the smallest viable implementation aligned with existing patterns.
4. Implement the change.
5. Run required gates:
   - invoke `validation-runner`
   - for Terraform behavior changes, invoke `terraform-plan`
6. If a required gate fails, fix and re-run gates. Escalate only if blocked.
7. Update relevant docs/indexes when discoverability changed.
8. Add/update task log when work is meaningful (invoke `task-log-update`).
9. Return a concise completion summary ending with a gate recap.

## Gate expectations

- A gate is PASS only when required checks complete successfully and plan intent matches expected behavior.
- A gate is FAIL when required checks fail, cannot be reviewed, or show unexpected behavior.
- If a required gate is skipped, record an explicit waiver with reason and residual risk.

## Constraints

- Do not mark complete before gates pass (or waiver is recorded).
- Do not broaden scope beyond task intent without user confirmation.
