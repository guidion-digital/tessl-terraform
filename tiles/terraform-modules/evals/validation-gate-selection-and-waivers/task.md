# Validation Execution Plan for Sprint Changes

## Problem/Feature Description

Your team completed a sprint with several parallel workstreams that touched different parts of the repository. Before merging the pull requests, a tech lead wants a written validation plan for each change set — something that makes explicit exactly which commands to run, what the success criteria are for each command, and how to handle any gate that can't be executed in the current environment.

One of the gates cannot be run right now because the test environment is temporarily unavailable due to an ongoing platform migration. The plan needs to handle this gracefully with a proper waiver rather than just skipping it silently.

The validation plan will be reviewed by the tech lead before any PR is merged.

## Output Specification

Produce a single markdown document `validation-plan.md` that covers all three change sets below. For each change set:
- State its change class
- List every validation command to run, in order
- Explain what each possible outcome means (pass vs fail)
- Include a waiver entry for any gate that cannot be run

The three change sets are:

**Change set A** — documentation update only:
- `docs/repo-indexes/modules.md` — added entry for new module
- `docs/index.md` — updated overview paragraph

**Change set B** — module source change:
- `modules/rds/main.tf` — added `backup_retention_period` variable and resource attribute
- `modules/rds/variables.tf` — added new variable definition

**Change set C** — coordinated module + example update:
- `modules/s3/main.tf` — added `versioning` block
- `modules/s3/variables.tf` — added `enable_versioning` variable
- `examples/test_app/main.tf` — updated module call to pass `enable_versioning = true`

Additionally, the `terraform -chdir=examples/test_app plan` gate for change set C cannot be run at this time because the test AWS environment is under maintenance. Include an appropriate waiver for this.
