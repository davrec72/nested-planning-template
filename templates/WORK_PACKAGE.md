# Work package template

Every substantive assignment coordinated through Foreman should bind to accepted planning state.

```text
work_package_id: <stable ID>
plan_id: <PlanID>
plan_ref: <exact accepted commit SHA>
role: <RoleID whose authority the package serves>
milestone: <MilestoneID>
parent_plan_ref: <exact parent PlanRef or none>
created_by_role: <RoleID>
return_to: <RoleID with final substantive authority>
```

## Objective

State one bounded outcome.

## In scope

- ...

## Out of scope

- ...

## Required inputs

- exact source/candidate revision(s);
- requirements/contracts;
- permitted tools/data/devices;
- relevant accepted evidence.

## Required return evidence

- exact revision/identity worked on;
- actions actually performed;
- tests/measurements/reviews actually executed;
- failures/skips/limitations;
- produced artifacts/links;
- unresolved blockers;
- whether parent/plan assumptions changed.

## Review requirements

State any required independent review, reviewer perspective, model/effort/tool limits, and what counts as independent.

## Future follow-up

```text
future_check_required: yes | no
condition/time: <exact condition or schedule>
Foreman_scheduled: <task ID or pending>
```

If future work is required, Foreman must actually schedule it. Do not write `will check later` without a scheduling mechanism.

## Acceptance boundary

State what this package may establish and what it cannot establish.

Completion of a work package does not automatically accept its milestone unless the returning Role has `ACCEPT_CHILD_MILESTONES` for that scope or another accepted authority grants milestone acceptance.
