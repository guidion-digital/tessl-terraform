# GitHub Index

## Purpose

Navigate repository automation and ownership files under `.github/`.

## Key files

- `.github/workflows/test.yaml`: PR workflow for `acc`, including Terrappy plan/test and release dry-run checks
- `.github/workflows/release.yaml`: apply and release workflow on pushes to `acc`
- `.github/workflows/destroy.yaml`: scheduled/manual destroy workflow for acceptance environments
- `.github/dependabot.yml`: Terraform and GitHub Actions dependency update policy
- `.github/CODEOWNERS`: repository ownership

## Search hints

- Terrappy workflows: `terrappy`
- Release automation: `release-workflows`
- Trigger branches: `acc`
