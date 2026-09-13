# Plan change template

Use this for every semantic planning or Role change.

Candidate creation/approval and publication are separate events. Follow `planning/PUBLICATION.md` and `planning/PUBLICATION_TRANSITIONS.md`.

```text
Semantic delta:
Affected milestones:
Affected roles:
Active work impact: none | continue | pause | redirect | supersede
Authority impact: none | binding change | scope change
Foreman dispatch required: yes | no
Controlling decision/evidence:
```

## Before the change

Resolve the validated publication-ref tip first:

```text
publication_ref:
prior_publication_commit:
prior_publication_id:
prior_plan_ref:
acting_role:
authority_source:
```

Do not use the newest default-branch head as a substitute for accepted state.

A proposed change cannot use its own new authority or governance to approve/publish itself.

## Exact semantic effect

Describe planning meaning, not merely the text diff.

## Candidate PlanRef

After the semantic change has a stable exact commit, record:

```text
candidate_plan_ref:
```

The candidate is not current merely because it exists or merges.

## Candidate approval

```text
approval_event:
approved_by_role:
approval_authority_source:
approved_scope:
```

Approval must bind the exact candidate. If content changes, obtain new approval.

## Active work handling

For every affected active package state one:

```text
continue | pause | redirect | supersede
```

Until publication succeeds, operational work remains governed by the prior accepted PlanRef.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

## Publication handoff

Prepare/review a successor publication carrier under the **predecessor accepted governance**.

```text
successor_publication_id:
successor_carrier_commit:
publication_ref:
prior_publication_commit:
prior_publication_id:
prior_plan_ref:
plan_ref: <candidate_plan_ref>
```

After the first publication, the successor carrier Git parent and all `CURRENT.prior_*` values must match the validated incumbent carrier.

Advance the publication ref non-force from that exact incumbent. If another publisher advances first, the stale carrier must fail/reconcile rather than win by timestamp/order.

## Foreman propagation payload

Only after successful publication send:

```text
publication_id:
publication_commit:
new_plan_ref:
prior_publication_id:
prior_plan_ref:
semantic_delta:
affected_roles:
affected_milestones:
active_work_impact:
authority_change:
controlling_links:
```

Foreman must match this payload to the exact validated publication transition and reconcile stale/duplicate/out-of-order notifications before applying transition-specific actions.

This notification is coordination, not approval or publication authority.