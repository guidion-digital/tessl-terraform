# Terraform Change Verification Script

## Problem/Feature Description

Your infrastructure team has been burned twice this quarter by Terraform changes that looked correct but produced unexpected results at apply time — one silent no-op (the edit never reached the right module path) and one accidental replace of a security group that was only supposed to be tagged. After reviewing the incidents, the team lead wants a standardized, reusable verification script that every engineer runs after making Terraform edits, before they mark any ticket as done.

The script should be ready to drop into any developer's checkout of this repository. It needs to handle the full verification sequence: confirm the environment is ready, run the plan in the right place, produce output that can be reasoned about programmatically, cross-check that the results match intent, and leave the workspace clean afterward. The team has standardized on a specific directory layout — all example/test configurations live under `examples/test_app`.

The script should also be accompanied by a short `README.md` that explains the pass/fail criteria, since new engineers often assume "no errors" means the plan succeeded.

## Output Specification

Produce:
- `verify-terraform.sh` — the reusable bash verification script
- `README.md` — a short guide covering when the script passes, when it fails, and how to interpret the output
