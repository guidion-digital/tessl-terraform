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
