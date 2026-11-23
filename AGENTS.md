# AGENTS.md: ML requests

Instructions for anyone who wants to propose an ML use case, for the platform
lead who handles the requests, and for their AI agents.

## What this repo is for

The **front door** for new ML use cases. Someone with an idea opens a GitHub
issue with the request form. The platform lead qualifies it and decides:
approved, deferred or declined. An approved request becomes **one YAML file**
in the platform repo's ML registry plus **one project repo** from the template.

Jargon in one line each:
- **Issue form**: a GitHub issue with fixed fields, like a web form.
- **Label**: a coloured tag on an issue; here it shows the request's status.
- **Risk tier**: how much harm a wrong prediction can do; it decides how strict the approval is.
- **ML registry**: a folder of YAML files in the platform repo, one per use case;
  the platform's Terraform reads them and sets up Azure.

## Where this repo sits in the overall process

| Step | What happens | This repo? |
|---|---|---|
| 0. Explore | Try the idea, no request needed | No |
| 1. Request | Fill in the issue form | **Yes** |
| 2. Qualify | Platform lead checks value, data, owner, risk tier → go / not now / no | **Yes** |
| 3. Data and priority | Data access and priority agreed | **Yes: tracked on the issue** |
| 4. Build | Project repo from the template; work happens there | Link only |
| 5. Run and review | First review date from the request | Link only |

## Folder structure

```
.github/ISSUE_TEMPLATE/ml-project-request.yml   the request form
.github/ISSUE_TEMPLATE/config.yml               no blank issues; link for "just exploring"
docs/process.md             steps 0-5, who does what, labels
docs/qualify-checklist.md   what the platform lead checks before "go"
docs/setup-checklist.md     after "go": form → registry YAML, project repo, hand-over
```

## The form and the registry file

Form fields marked **"→ registry"** use the same names and formats as the
registry YAML (`registry/ml_use_cases/<department>__<use_case_id>.yaml`):
`use_case_id`, `display_name`, `department`, `owner`, `risk_tier`, `reads`,
`predictions_table`, `gpu`. `github_repo` is added at setup. The other fields
(problem, usage, sponsor, sensitivity, review date, what was explored) are only
for the decision. The mapping table is in `docs/setup-checklist.md`.

## Workflow

1. **Requester**: *Issues → New issue → ML project request*. The issue gets label `new`.
2. **Platform lead**: sets `qualifying`, copies `docs/qualify-checklist.md` into
   a comment and goes through it with the requester.
3. Decision: `approved`, `deferred` or `declined`, with a short comment why.
4. If approved: follow `docs/setup-checklist.md` (registry pull request in the
   platform repo, project repo, data access, hand-over), then set `set-up` and
   close the issue with links.

Labels: `new` → `qualifying` → `approved` / `deferred` / `declined` → `set-up`.
Create them once under *Issues → Labels*.

There is no automation yet. A future `on-approved.yml` (form → registry pull
request) is only described in `docs/process.md`.

## Commands

None needed. To preview the form, push to GitHub and open *Issues → New issue*.

## Rules (what not to do)

- **No secrets and no real company data** in issues or files.
- Generic examples only: use case `tool-wear`, department `manufacturing`.
- Do not start a project repo or infrastructure before the request is `approved`.
- Keep the form short: only fields the platform lead needs to decide or set up.
- **Form and registry stay in sync**: when the registry schema gets a new or
  changed field, update the form and the table in `docs/setup-checklist.md`.
- In `config.yml`, replace `example-org` in the link with your organization.
- When you change the form, labels or process, update this file in the same change.
