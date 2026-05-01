# Deterministic execution contract

Apply this contract to all repository work.

1. Classify the change type before implementing (`docs-only`, `terraform-module`, `example-terraform`, `ci-workflow`, `mixed`).
2. Read only the files needed for the task. Prefer indexes and overview files before implementation files.
3. Choose the smallest viable implementation that matches existing repository patterns.
4. Run mandatory validation gates for the change class before declaring completion.
5. If a mandatory gate fails, fix the issue, narrow scope, or escalate.
6. If a required gate is skipped, record a waiver with: skipped gate, reason, residual risk, and acceptance context.

## Source of truth order

When sources disagree, resolve in this order:

1. Executable tests and validation commands
2. Current codebase
3. Current repository documentation
4. Stable memory
5. Episodic memory

Memory is advisory, never authoritative.
