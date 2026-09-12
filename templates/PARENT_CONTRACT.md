# Parent contract template

This contract defines what a parent plan expects from one child milestone and what authority is delegated across that boundary.

```text
contract_id: <stable ID>
parent_plan_id: <PlanID>
parent_plan_ref: <exact accepted parent PlanRef>
parent_milestone: <MilestoneID>
child_repository: <owner/repo or same-repo path>
child_plan_id: <PlanID>
child_plan_path: <path>
child_scope_owner_role: <RoleID>
```

## Required outcome

State exactly what must become true for the parent milestone.

## Acceptance criteria

- ...

## Required evidence

- ...

## Delegated scope

State what the child may plan/decide/execute without returning to the parent.

## Explicit exclusions

State what remains outside child authority, including shared contracts, spending, release, data/device access, cross-project scope, or other retained parent decisions.

## Delegation capabilities

List only capabilities actually granted:

```text
DECOMPOSE_SCOPE
CREATE_SUBROLES
BIND_SUBROLE_HOLDERS
DELEGATE_DECISIONS
ACCEPT_CHILD_MILESTONES
```

Omitted capability = not granted.

## Parent acceptance authority

```text
parent_acceptance_role: <RoleID>
```

Unless explicitly delegated elsewhere, this Role accepts the parent milestone after reviewing child evidence.

## Escalation triggers

The child must escalate when:

- it cannot meet the required outcome within delegated scope;
- the parent-facing contract needs to change;
- shared contracts owned above the child need modification;
- requested work exceeds delegated permissions/resources;
- final authority conflicts or becomes ambiguous.

Add project-specific triggers here.

## Notification triggers

Notify the parent when:

- this contract changes;
- delegated authority changes;
- child identity changes;
- the child reaches parent-facing readiness/acceptance;
- an escalation trigger fires.

Internal child-plan changes that preserve this contract do not require parent plan churn.
