# AGENTS.md: ML requests

Instructions for anyone who wants to propose an ML use case, for the platform
lead who handles the requests, and for their AI agents.

## What this repo is for

The **front door** for new ML use cases. Someone with an idea opens a GitHub
issue with the request form. The platform lead qualifies it and decides:
approved, deferred or declined. Approved requests get set up (Azure + project repo).

Jargon in one line each:
- **Issue form**: a GitHub issue with fixed fields, like a web form.
- **Label**: a coloured tag on an issue; here it shows the request's status.
- **Risk tier**: how much harm a wrong prediction can do; it decides how strict the approval is.

## Where this repo sits in the overall process

| Step | What happens | This repo? |
|---|---|---|
| 0. Explore | Try the idea, no request needed | No |
| 1. Request | Fill in the issue form | **Yes** |
| 2. Qualify | Platform lead checks value, data, owner, risk tier → go / not now / no | **Yes** |
| 3. Data and priority | Data access and priority agreed | **Yes: tracked on the issue** |
| 4. Build | Project repo from the template; work happens there | Link only |
| 5. Run and review | Review dates from the request | Link only |

## Folder structure (built in milestone 6)

```
.github/ISSUE_TEMPLATE/ml-project-request.yml   the request form
.github/ISSUE_TEMPLATE/config.yml               blank issues disabled
docs/process.md             steps 0-5, who does what, labels
docs/qualify-checklist.md   what the platform lead checks before "go"
docs/setup-checklist.md     after "go": project repo, CDP block, GitHub variables
```

## Workflow

1. **Requester**: *Issues → New issue → ML project request*. Fill in: use case
   name, problem and value, owner, sponsor, risk tier, data and sensitivity,
   CPU or GPU, how predictions are used, review date, what was explored.
2. The issue gets label `new`.
3. **Platform lead**: sets `qualifying` and works through `docs/qualify-checklist.md`.
4. Decision: `approved`, `deferred` or `declined`, with a short comment why.
5. If approved: follow `docs/setup-checklist.md`, then set `set-up` and close the issue.

Labels: `new` → `qualifying` → `approved` / `deferred` / `declined` → `set-up`.

There is no automation yet. A future `on-approved.yml` is only described in `docs/process.md`.

## Commands

None needed. To preview the form, push to GitHub and open *Issues → New issue*.

## Rules (what not to do)

- **No secrets and no real company data** in issues or files.
- Generic examples only: use case `tool-wear`, department `manufacturing`.
- Do not start a project repo or infrastructure before the request is `approved`.
- Keep the form short: only fields the platform lead needs to decide.
- When you change the form, labels or process, update this file in the same change.
