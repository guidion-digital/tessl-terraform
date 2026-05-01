---
name: terraform-plan
description: |
  Use when `.tf` or `.tfvars` files have been edited, added, or removed and
  you need to verify that the code changes produce the intended Terraform
  plan before the task is considered complete. Runs `terraform plan` in
  `examples/test_app` and cross-checks the result against the change set
  you expected your edits to cause. This is a gate: do not declare a
  Terraform task done without passing it.
---

# Verify Terraform Changes with Plan

Confirm that edits to Terraform code produce the infrastructure changes you
expect — no more, no less. Treat the outcome as a gate.

## Pre-flight

Before running plan, verify the environment. If any check fails, STOP and
report the failure to the user; do not proceed.

1. **Terraform is installed:** `terraform version`.
2. **AWS session is valid:** `aws sts get-caller-identity`. Failures here
   usually mean missing credentials, expired SSO, or the wrong `AWS_PROFILE`.
   Ask the user to authenticate; do not guess the profile.
3. **Plan directory exists:** use `examples/test_app` relative to the repo
   root. If this directory does not exist, ask the user which directory to
   run the plan in. Do not silently fall back to another path.

## Procedure

All commands run from the plan directory (default `examples/test_app`).

1. **Initialize (idempotent):**

   ```
   terraform init -input=false
   ```

2. **Generate a machine-readable plan:**

   ```
   terraform plan -input=false -lock=false -out=tfplan
   terraform show -json tfplan > tfplan.json
   ```

   Use `tfplan.json` as the source of truth. The stdout rendering is lossy
   and hard to reason about programmatically.

3. **State your expectation, then read the plan.** Before opening
   `tfplan.json`, write down the concise list of changes you _expected_ your
   edit to cause (e.g. "add one `aws_iam_policy`, update the role attached
   to `aws_lambda_function.api`"). Then extract from `tfplan.json`, for each
   entry under `.resource_changes[]`:
   - `address`
   - `change.actions` (e.g. `["create"]`, `["update"]`, `["delete", "create"]`)
   - for updates/replaces: which attributes under `change.before`/`change.after`
     differ, and any `change.replace_paths`

4. **Cross-check:** every expected change must appear in the plan, and every
   planned change must be explained by an expected change. Mismatches mean
   the task is NOT complete.

5. **Clean up:**
   ```
   rm -f tfplan tfplan.json
   ```

## Pass criteria

A pass is **only** when every planned action matches what you intended to
change. "No errors" is not enough; a plan can succeed and still do the wrong
thing. A plan with zero changes is a FAIL if you expected changes — it
usually means your edit didn't take effect (wrong module path, unmodified
variable, etc.).

## Common failure modes

- Unexpected `replace` / forced-new on a resource you only meant to tweak —
  check `change.replace_paths` to find the attribute causing it.
- Unexpected `delete` on stateful resources (RDS, S3, EFS, DynamoDB) — almost
  never intended; investigate before proceeding.
- Zero changes when you expected some — your edit is probably unreached
  (wrong directory, conditional `count`/`for_each`, variable default).
- Changes to resources you didn't touch — often points to a variable default
  change, provider upgrade, or shared local being mutated.

## Reporting back

When the plan passes, tell the user briefly which resources change and how
(e.g. "1 create, 2 updates, 0 destroys; all match the intended edit"). When
it fails, report the specific mismatch and stop — do not attempt further
edits until the user has seen the discrepancy.
