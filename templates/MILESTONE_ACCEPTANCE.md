# Milestone acceptance template

Use this record when an authorized acceptance authority concludes that one milestone's stated outcome and acceptance criteria have been satisfied.

This is separate from work completion, review completion, evidence production, and the roadmap's status class.

```text
acceptance_id: <stable ID>
plan_id: <PlanID>
plan_ref: <exact accepted PlanRef whose milestone contract is being accepted>
milestone_id: <MilestoneID>
accepted_by_role: <RoleID>
acceptance_authority_source: <accepted source granting this Role acceptance authority>
accepted_at: <time or durable event reference>
supersedes: <prior acceptance record or none>
```

## Milestone contract being accepted

```text
Outcome:
Acceptance criteria:
```

Quote or link the exact contract from the bound PlanRef. Do not silently accept a later or differently worded criterion.

## Accepted evidence

List exact evidence/revisions/measurements/reviews relied upon.

- ...

Evidence existing is not itself acceptance. State why the evidence satisfies each acceptance criterion.

## Criterion-by-criterion determination

| Criterion | Evidence | Determination |
|---|---|---|
| `<criterion>` | `<exact evidence>` | `satisfied` |

Do not omit a required criterion. If a criterion is not satisfied, do not issue an acceptance record.

## Limitations / residuals

Record limits that remain compatible with the milestone's stated criteria. Do not weaken the criteria here.

- ...

## What this acceptance does not establish

Unless separately required by the milestone contract, this record does not imply that:

- every attempted work package succeeded;
- every listed implementation step was necessary;
- the assigned delivery Role also possessed acceptance authority;
- downstream milestones are accepted;
- unrelated safety, release, spending, data, or deployment authority is granted.

## Roadmap projection

After this acceptance is durable, the roadmap may project the milestone as `MILESTONE_DONE` and link this record as the reason for that status.

A roadmap class change without a valid acceptance record does not create acceptance.
