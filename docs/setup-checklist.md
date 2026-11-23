# Setup checklist (after "go")

For the platform lead. Turns an approved request into a working project:
**one YAML file** in the platform repo and **one repo** from the template.
Nobody writes Terraform for it.

Example: use case `tool-wear` in department `manufacturing`.

## 1. From the form to the registry file

Every form field marked "→ registry" goes into
`registry/ml_use_cases/<department>__<use_case_id>.yaml` in the platform repo
(copy an existing file there):

| Form field | Registry field | Example |
|---|---|---|
| Use case name | `use_case_id` | `tool-wear` |
| Readable name | `display_name` | `Tool wear prediction` |
| Department | `department` | `manufacturing` |
| Model owner | `owner` | `"[model owner]"` |
| Risk tier (as agreed at qualification) | `risk_tier` | `decision_support` |
| Data the model needs | `reads` (a list) | `manufacturing.gold.fact_machine_sensors` |
| Predictions table (empty = `ml_<name>_predictions`, hyphens become `_`) | `predictions_table` | `ml_tool_wear_predictions` |
| Does the model need a GPU? | `gpu` | `false` |
| (set by you, step 2 below) | `github_repo` | `example-org/ml-tool-wear` |

Also set `schema_version: "1.0.0"` and `status: active`.

The result looks like this:

```yaml
# yaml-language-server: $schema=../schema/ml_use_case.schema.json
schema_version: "1.0.0"
use_case_id: tool-wear
display_name: Tool wear prediction
department: manufacturing
status: active
owner: "[model owner]"
github_repo: "example-org/ml-tool-wear"
risk_tier: decision_support
gpu: false
reads:
  - manufacturing.gold.fact_machine_sensors
predictions_table: ml_tool_wear_predictions
```

## 2. The checklist

- [ ] **Project repo:** create `ml-<use_case_id>` from the `ml-project-template`
      repo (*Use this template*). Give the model owner and team access.
- [ ] **Registry file:** open a pull request in the platform repo with the file
      above. If the department has no `registry/ml_workspaces/<department>.yaml`
      yet, add it in the same pull request. Follow the platform repo's
      onboarding checklist (checks, `terraform plan`, approval, apply).
- [ ] **Data access:** after apply, the `data_access_todo` output lists what the
      data owners must grant in Fabric (read on `reads`, write on
      `predictions_table`). Ask them, link their answers here.
- [ ] **Hand-over:** give the project team the `github_variables` output (five
      IDs, stored as GitHub *variables*, not secrets):
      `AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`,
      `AZURE_RESOURCE_GROUP`, `AZURE_ML_WORKSPACE`.
- [ ] **Approval gate:** in the project repo, *Settings → Environments* →
      `production`, with the reviewer from qualification as required reviewer.
- [ ] **Project settings:** in the project repo's `config.yml`, `model.name` =
      `use_case_id` and `scoring.predictions_table` = the registry's
      `predictions_table`. In `model-card.md`: owner, risk tier, first review date.
- [ ] **Close:** comment with links to the project repo and the registry pull
      request, set the label `set-up`, close this issue.
