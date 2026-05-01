---
name: validation-runner
description: |
  Use when repository changes are complete and you need to run and report the
  required validation gates for the applicable change class (`docs-only`,
  `terraform-module`, `example-terraform`, `ci-workflow`, or `mixed`).
---

# Run required validation gates

Run only the gates required by the change class and report results as a concise gate recap.

## Procedure

1. Classify the change as one of: `docs-only`, `terraform-module`, `example-terraform`, `ci-workflow`, `mixed`.
2. For `mixed`, run the union of gates for all relevant classes.
3. Execute canonical commands from the `validation-gates` rule.
4. For Terraform plan commands using `-detailed-exitcode`:
   - `0` = no diff (PASS)
   - `2` = diff exists (PASS only if diff matches intended changes)
   - any other code = FAIL
5. If a gate cannot run, record a waiver containing skipped gate, reason, residual risk, and acceptance context.
6. End with a compact gate summary listing command scope, result, and waivers.

## Reporting format

Use concise output:

- `Gates: terraform fmt -check -recursive passed; terraform -chdir=. validate passed; terraform -chdir=examples/test_app plan -detailed-exitcode=2 reviewed (expected diff).`
- `Gates: links checked; markdown lint not run (waived: tooling unavailable, low risk).`
