# Work package template

Every substantive assignment coordinated through Foreman should bind to accepted planning state.

```text
work_package_id: <stable ID>
reference_contract: qualified-reference-v1
repository_identity: {scheme: github-repository-id-v1, authority: <GitHub host>, id: <numeric repository ID>}
plan_id: <PlanID>
plan_ref: <exact accepted commit SHA>
role: <RoleID whose authority the package serves>
milestone: <MilestoneID>
parent_plan: <qualified parent plan reference or none>
parent_plan_ref: <exact accepted parent relationship pin or none>
created_by_role: <RoleID>
return_to: <RoleID with final substantive authority>
```

Local IDs inherit this package's repository/PlanID and their field's kind. Every cross-plan Role, target, parent contract or return authority uses a full qualified reference under `planning/REFERENCES.md`. Bind each relied-upon external authority's exact PlanRef separately; the package `plan_ref` names only its own plan. For nested use also resolve the current parent PlanRef and verify the pinned relationship still applies. A locator or shared Role name is not authority.

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

Completion of a work package is a report/evidence event, not milestone acceptance. Even when the returning Role is also authorized to accept the milestone, issue a separate milestone acceptance record that binds the exact criteria and accepted evidence. Use `templates/MILESTONE_ACCEPTANCE.md`.

Never infer acceptance merely from:

- a worker saying `done`;
- a clean review;
- passing tests outside their stated scope;
- merge of an implementation PR;
- the assigned delivery Role being the same holder as an accepting Role.
