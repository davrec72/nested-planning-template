# Parent contract template

This contract defines what a parent plan expects from one child milestone and what authority is delegated across that boundary.

```text
contract_id: <stable ID>
reference_contract: qualified-reference-v1
parent_plan: <qualified plan reference>
authority_baseline_plan_ref: <exact prior accepted parent PlanRef authorizing this relationship change>
parent_authority_role: <qualified role reference>
parent_authority_source: <exact pre-existing authority/delegation source at that baseline>
parent_milestone: <qualified milestone reference in parent_plan>
child_plan: <qualified plan reference>
child_repository_locator: <readable owner/repo or URL; locator only>
child_plan_path: <path>
child_scope_owner_role: <qualified role reference in child_plan>
```

This parent-side contract does not contain its own accepted relationship SHA. After the exact candidate is approved and published, its accepted `parent_relationship_plan_ref` is learned from publication evidence; the child records that SHA as `parent_plan_ref`. The baseline may not yet contain this new contract. Follow the finite creation/update sequence in `planning/REFERENCES.md`.

The qualified contract identity is `parent_plan` plus `object_kind: contract` and this `contract_id`. `parent_plan` fixes the context of any short local parent ID; child objects still use full qualified references. Repository/plan paths are locators. A reference or named intended child Role does not establish accepted child state or grant authority.

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
parent_acceptance_role: <local parent RoleID or qualified role reference>
parent_acceptance_authority_source: <independently accepted source; qualify and bind its own exact PlanRef if external>
```

Unless explicitly delegated elsewhere, this Role accepts the parent milestone after reviewing child evidence.

Resolve that Role's exact accepted authority revision separately when issuing acceptance; the contract cannot grant authority merely by naming the Role. Do not embed an unknown future containing SHA here.

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
