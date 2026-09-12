# Plan change template

Use this for every semantic planning or role change.

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

State the accepted PlanRef and authority that exists before this proposal.

```text
prior_plan_ref:
acting_role:
authority_source:
```

A proposed change cannot use its own new authority to approve itself.

## Exact roadmap/role effect

Describe the semantic change, not merely the text diff.

Examples:

- `M2 no longer depends on M1C`;
- `IntegrationLead now decides D3`;
- `GlassesLead holder changes from X to Y; scope unchanged`;
- `M1B becomes a child plan owned by GlassesLead`.

## Active work handling

For every affected active package, state one:

```text
continue
pause
redirect
supersede
```

Do not assume a plan merge silently cancels work.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

If a parent-facing boundary changes, update/notify the parent under `planning/NESTING.md`.

## Foreman propagation payload

After acceptance/merge, Foreman must receive:

```text
new_plan_ref:
semantic_delta:
affected_roles:
affected_milestones:
active_work_impact:
authority_change:
controlling_links:
```

This notification is coordination, not a new approval request.
