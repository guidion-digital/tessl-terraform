# Terraform Modules Tile

This tile is the canonical agent context for developing Terraform modules in this repository.

It combines:

- **Rules** for deterministic execution, validation gates, escalation boundaries, and definition of done
- **Skills** for running Terraform plan checks, task workflow execution, validation running, and task-log updates
- **Repository indexes** for targeted file discovery without broad scanning

## Use this as the canonical source

Legacy agent docs were migrated into this tile and are no longer required.

## Repository indexes

- [Repo root index](repo-indexes/repo-root.md)
- [Modules index](repo-indexes/modules.md)
- [Examples index](repo-indexes/examples.md)
- [GitHub index](repo-indexes/github.md)

## Rule set summary

- Deterministic execution contract
- Validation gates by change class
- Decision boundaries and escalation
- Definition of done

- Terraform plan verification gate
