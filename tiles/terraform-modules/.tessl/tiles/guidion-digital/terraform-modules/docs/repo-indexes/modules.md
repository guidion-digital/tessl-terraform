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
