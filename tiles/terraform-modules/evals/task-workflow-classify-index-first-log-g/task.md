# Add Documentation for the deepmerge Utility Module

## Problem/Feature Description

A new engineer joining the platform team has flagged that the `modules/deepmerge/` utility module is poorly documented. The module itself is stable and widely used internally — it merges YAML maps/objects via `utils_deep_merge_yaml` — but the only documentation that exists is the sparse inline comments in the Terraform files themselves. There's no explanation in the modules index of when to use it, what problem it solves, or what its key inputs/outputs are.

The team lead has asked you to add a proper description of the `deepmerge` module to the repository documentation so it shows up correctly when engineers look for merge utilities. The existing module source code should not be changed — this is purely a documentation task to improve discoverability.

Complete this task as you normally would, including any record-keeping that the team expects after meaningful work.

## Output Specification

Updated repository documentation files reflecting the improved `deepmerge` module description. Include any task record-keeping your workflow requires.

## Input Files

The following files represent the current state of the repository's documentation and the deepmerge module. Extract them before beginning.

=============== FILE: docs/repo-indexes/modules.md ===============
# Modules Index

## Purpose

Navigate local helper modules under `modules/` that affect root-module behavior.

## Read This When

- task changes generated API behavior
- task changes event triggers or per-method API settings
- root-module changes delegate behavior into local submodules

## Key Modules

- `modules/deepmerge/`: merges maps/objects via `utils_deep_merge_yaml`
- `modules/event_triggers/`: EventBridge rules and SQS event source mappings for Lambdas
- `modules/method_settings/`: per-endpoint API Gateway method settings fan-out

## Key Files

- `modules/deepmerge/main.tf`
- `modules/deepmerge/variables.tf`
- `modules/event_triggers/main.tf`
- `modules/event_triggers/variables.tf`
- `modules/method_settings/main.tf`
- `modules/method_settings/method_settings_loop/main.tf`

## Search hints

- OpenAPI merge: `utils_deep_merge_yaml`, `merged`
- Event wiring: `aws_cloudwatch_event_rule`, `aws_lambda_event_source_mapping`
- Method settings: `aws_api_gateway_method_settings`

=============== FILE: docs/repo-indexes/repo-root.md ===============
# Repo Root Index

## Purpose

Navigate the Terraform module at the repository root.

## Read This When

- task changes module behavior
- task changes module inputs or outputs
- task needs the public module contract

## Key Files

- `main.tf`: core resources, Lambda assembly, API Gateway construction, OpenAPI generation, VPC/WAF hooks, log subscriptions
- `variables.tf`: module inputs for lambdas, API behavior, DNS, WAF, supporting resources, ElastiCache, secrets, SSM
- `outputs.tf`: module outputs for OpenAPI, Lambda artifacts, VPC, method settings, secrets, ElastiCache
- `dns.tf`: ACM validation, custom domains, base path mappings, Route53 records
- `memcached.tf`: optional ElastiCache cluster wiring
- `versions.tf`: provider requirements and alias expectations
- `README.md`: public module description
- `AGENTS.md`: agent entrypoint

## Search hints

- Lambda resources: `aws_lambda_function`, `aws_lambda_alias`
- VPC/security groups: `aws_security_group`, `aws_vpc_security_group_`
- OpenAPI generation: `paths_spec`, `x-amazon-apigateway`
- DNS/ACM: `aws_api_gateway_domain_name`, `aws_route53_record`, `acm_validations`
- Data stores: `module.elasticache`, `dynamodb_tables`, `sqs_queues`

=============== FILE: modules/deepmerge/variables.tf ===============
variable "base" {
  description = "The base map to merge into"
  type        = any
}

variable "override" {
  description = "The override map whose values take precedence"
  type        = any
}

=============== FILE: modules/deepmerge/main.tf ===============
# Deep merges two maps, with override values taking precedence over base.
# Uses the utils_deep_merge_yaml external function.
locals {
  merged = yamldecode(
    provider::utils::deep_merge_yaml(
      yamlencode(var.base),
      yamlencode(var.override)
    )
  )
}

output "merged" {
  description = "The deeply merged result"
  value       = local.merged
}
