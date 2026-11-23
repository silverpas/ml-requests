# Qualify checklist (step 2)

For the platform lead, before saying "go". Copy it into a comment on the
request issue and tick it together with the requester.

```markdown
**Value**
- [ ] The problem and its value are clear (rough numbers are fine).
- [ ] Someone will use the predictions, and we know how (report, alert, screen).
- [ ] ML is the right tool: a simple rule or a report would not do the job.

**People**
- [ ] There is a model owner who has time to build, run and review it.
- [ ] There is a reviewer for the approval gate (not the owner).

**Risk**
- [ ] Risk tier agreed: exploration / decision_support / production_critical.
- [ ] production_critical: operations sign-off and a fallback plan are possible.
- [ ] Personal data: privacy check done or planned.

**Data**
- [ ] The data exists, and we know its tables (<domain>.<layer>.<table>),
      or a data request is raised and linked here.
- [ ] The data owners are known and willing to grant access.
- [ ] There are enough examples of what we want to predict (e.g. enough failures).

**Fit**
- [ ] CPU is enough, or the GPU need is real (deep learning) and the
      department's workspace has, or can get, a GPU cluster.
- [ ] Predictions can be scored in batch (e.g. nightly). Real-time answers
      are out of scope for now.
- [ ] First review date agreed.

**Decision:** approved / deferred / declined, because ...
```

## Tips

- **Deferred is not no.** Write what would change the answer, e.g. "when the
  sensor data is in the platform".
- **Start small.** If the idea is big, approve a first slice with one clear
  prediction and one user.
- **Exploration tier** is fine for "let's see if it works": it gets the setup
  but can never go live without a new qualification.
