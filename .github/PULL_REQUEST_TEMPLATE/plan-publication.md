## Plan publication

Use this only for the mechanical publication step defined by `planning/PUBLICATION.md`.

This PR must not introduce new semantic planning content. If semantic content changed after approval, stop and create/review a new candidate instead.

## Current publication baseline

```text
prior_publication_id:
prior_publication_commit:
prior_plan_ref:
```

These values must match the valid `planning/CURRENT.md` immediately before publication.

## Candidate being published

```text
candidate_plan_ref:
plan_id:
grammar:
approval_basis: role | founding | parent
approval_event:
approved_by_role: <RoleID or none>
approval_authority_source: <accepted source or none>
founding_record: <locator or none>
parent_authority_source: <locator or none>
```

The approval event must cover the exact `candidate_plan_ref`.

## Publication actor

```text
publisher_identity:
publication_authority_source:
```

Repository write access alone is not publication authority.

## Validation checklist

- [ ] `candidate_plan_ref` exists and contains the exact planning state that was approved.
- [ ] The approval event names that exact candidate SHA.
- [ ] Approval authority existed before the candidate's new authority/scope would become current, except for the one-time root founding or parent bootstrap explicitly allowed by `planning/PUBLICATION.md`.
- [ ] `planning/CURRENT.md` still matches `prior_publication_id` and `prior_plan_ref`.
- [ ] The publication chains to the prior record with the correct `prior_publication_commit`.
- [ ] This publication change does not add or alter semantic plan/Role content beyond the already-approved candidate.
- [ ] `publisher_identity` is attributable and `publication_authority_source` permits the publication action.
- [ ] If the baseline changed, this PR is treated as stale and is reconciled/re-approved as needed rather than merged by timestamp/order.

## After publication

Once this publication is durably accepted/written, the `plan_ref` named by the new `planning/CURRENT.md` becomes the current accepted PlanRef.

Then send Foreman the publication ID, new PlanRef, semantic delta, affected scopes, and active-work impact. Publication is the trigger for operational propagation; candidate merge/staging alone is not.