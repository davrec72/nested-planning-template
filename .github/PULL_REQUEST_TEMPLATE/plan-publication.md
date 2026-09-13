## Plan publication transition

Use this checklist to review one proposed successor carrier for `plan-publication-v1`.

A normal semantic PR/merge is **not** the publication event. Publication occurs only when the configured publication ref advances non-force from the exact incumbent carrier to the reviewed successor carrier under `planning/PUBLICATION.md` and `planning/PUBLICATION_TRANSITIONS.md`.

## Validated predecessor

```text
publication_ref: refs/heads/plan-publications
prior_publication_commit:
prior_publication_id:
prior_plan_ref:
predecessor_governance_ref: <normally prior_plan_ref>
```

These values must come from validated publication-ref history, not an unpublished default-branch copy of `CURRENT` or governance files.

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

The approval event must cover the exact candidate SHA.

## Successor carrier

```text
successor_carrier_commit:
successor_carrier_parent: <must equal prior_publication_commit after first publication>
CURRENT.prior_publication_commit:
CURRENT.prior_publication_id:
CURRENT.prior_plan_ref:
```

## Publication actor

```text
publisher_identity:
publication_authority_source:
```

Repository write access alone is not publication authority.

## Validation checklist

- [ ] `candidate_plan_ref` exists and contains the exact approved planning state.
- [ ] Approval authority was valid before the candidate's new authority/scope would become current, except for the bounded founding/parent bootstrap path.
- [ ] Transition validation uses the predecessor accepted PlanRef's publication/governance rules; candidate governance changes do not validate themselves.
- [ ] Successor carrier Git parent equals the actual incumbent carrier after the first publication.
- [ ] `CURRENT.prior_*` exactly matches the validated predecessor record.
- [ ] The carrier changes publication state only; it does not smuggle new semantic planning content into the candidate.
- [ ] Publisher identity is attributable and publication authority permits this action.
- [ ] Publication ref advancement is non-force from the exact incumbent carrier. A stale sibling carrier must be rejected rather than winning by timestamp/order.
- [ ] Replay of old `CURRENT` contents is rejected unless represented as a new authorized transition from the actual incumbent.
- [ ] The propagation payload binds `publication_id`, `publication_commit`, `new_plan_ref`, `prior_publication_id`, and `prior_plan_ref` to this exact transition.

## After successful ref advancement

The `plan_ref` named by the validated publication-ref tip becomes current accepted planning state.

Only then send Foreman the transition-bound semantic delta and active-work impact. Candidate merge/staging alone is not a propagation trigger.