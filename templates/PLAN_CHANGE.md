# Plan change template

Use this for every semantic planning or Role change.

A semantic candidate and the publication that makes it current are separate events. Follow `planning/PUBLICATION.md`.

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

Resolve the current publication first.

```text
prior_publication_id:
prior_publication_commit:
prior_plan_ref:
acting_role:
authority_source:
```

`prior_plan_ref` must come from the valid `planning/CURRENT.md`, not from the newest branch head.

A proposed change cannot use its own new authority to approve itself.

## Exact roadmap/role effect

Describe the semantic change, not merely the text diff.

Examples:

- `M2 no longer depends on M1C`;
- `IntegrationLead now decides D3`;
- `GlassesLead holder changes from X to Y; scope unchanged`;
- `M1B becomes a child plan owned by GlassesLead`.

## Candidate PlanRef

After the semantic change has been merged/staged, record the exact resulting commit:

```text
candidate_plan_ref:
```

This commit is not yet the current accepted PlanRef merely because it exists or was merged.

The approval event must name this exact candidate. If candidate content changes, obtain a new approval.

## Candidate approval

```text
approval_event:
approved_by_role:
approval_authority_source:
approved_scope:
```

The approving authority must already be valid under `prior_plan_ref` or another already-valid authority source. The candidate cannot create the authority used to approve itself.

## Active work handling

For every affected active package, state one:

```text
continue
pause
redirect
supersede
```

Do not assume a candidate merge silently cancels or redirects work. Until publication, operational work remains governed by the prior current PlanRef.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

If a parent-facing boundary changes, update/notify the parent under `planning/NESTING.md`.

## Publication

After candidate approval, publish the candidate through `planning/CURRENT.md` under `planning/PUBLICATION.md`.

Immediately before publication verify:

```text
CURRENT.publication_id == prior_publication_id
CURRENT.plan_ref == prior_plan_ref
```

If either check fails, stop. Reconcile the candidate against the newer accepted state and determine whether re-review/re-approval is required.

The publication record must identify:

```text
publication_id:
plan_ref: <candidate_plan_ref>
prior_plan_ref:
prior_publication_id:
prior_publication_commit:
approval_event:
publisher_identity:
publication_authority_source:
```

## Foreman propagation payload

Only after a valid publication makes the candidate current should Foreman receive the operational propagation payload:

```text
publication_id:
new_plan_ref:
prior_plan_ref:
semantic_delta:
affected_roles:
affected_milestones:
active_work_impact:
authority_change:
controlling_links:
```

This notification is coordination, not a new approval request.

A merged/staged but unpublished candidate must not be propagated as current planning state.