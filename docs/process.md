# From idea to running model

The whole path in six steps. Only two points have control (step 2 "qualify"
and the approval gate in step 4); everything else is self-service.

| Step | What happens | Who | Where |
|---|---|---|---|
| 0. Explore | Try the idea, no request needed | Anyone | Fabric notebooks, a laptop |
| 1. Request | Fill in the request form | Requester | This repo: an issue |
| 2. Qualify | Is there value? Is ML the right tool? Owner and risk tier | Platform lead + requester | This repo: the same issue |
| 3. Data and priority | Is the data in the platform? Who grants access? When do we start? | Platform lead, data owners | The issue, then Fabric |
| 4. Build | Train, evaluate, approve a model | Model owner and team | The project repo |
| 5. Run and review | Nightly predictions; every quarter: keep, retrain or retire? | Model owner | The project repo |

## 0. Explore (optional)

Trying an idea needs no request: a notebook in Fabric or on your laptop is fine.
Use only data you are already allowed to see. Open a request when the idea
looks worth a real project, and tell us what you tried.

## 1. Request

*Issues → New issue → ML project request.* The form asks for the problem, how
the predictions will be used, the data, an owner and a first guess of the risk
tier. Don't worry about fields you can't fill in: the platform lead helps.
The issue gets the label `new`.

## 2. Qualify

The platform lead sets `qualifying` and goes through
[qualify-checklist.md](qualify-checklist.md) with the requester, in comments
or in a short call. The answer is one of:

- `approved`: go. Continue with step 3 and the setup.
- `deferred`: good idea, not now (data missing, no owner, other priorities).
  Say what would change the answer.
- `declined`: no, with a short reason (no value, no need for ML, too risky).

**Risk tiers** decide how strict later steps are:

| Tier | Example | Before going live |
|---|---|---|
| `exploration` | Analysis, prototypes | Cannot go live |
| `decision_support` | Predictions shown in reports | Owner + reviewer approve |
| `production_critical` | Model affects machines or operations | Owner + reviewer + operations sign-off, local fallback plan |

## 3. Data and priority

- Data already in the platform: its owner grants read access (after setup).
- Data not in the platform yet: raise a data request with the data team and
  link it on the issue. The project waits for it.

## Setup (after "go")

The platform lead follows [setup-checklist.md](setup-checklist.md): one YAML
file in the platform repo's ML registry, one project repo from the template,
the IDs handed over. Then the label becomes `set-up` and the issue is closed
with links to both.

## 4 and 5. Build, run and review

They happen in the project repo, see its `AGENTS.md`. The project repo opens
a review issue every quarter; the first review date comes from this request.

## Labels

Create them once in the repo (*Issues → Labels*); the form adds `new` only if
it exists.

| Label | Meaning |
|---|---|
| `new` | Just submitted |
| `qualifying` | The platform lead is looking at it |
| `approved` | Go |
| `deferred` | Not now (reason in a comment) |
| `declined` | No (reason in a comment) |
| `set-up` | Registry file merged and project repo created; issue closed |

## Later: automation (not built)

A workflow `on-approved.yml` could, when the label `approved` is added, read
the form's answers and open the pull request with the registry YAML in the
platform repo. It is left out on purpose: first run the process by hand on a
few real requests, then automate what turns out to be repetitive.
