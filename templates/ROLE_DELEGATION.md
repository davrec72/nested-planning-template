# Role delegation template

Use this record when one accepted Role delegates authority to another Role.

```text
delegation_id: <stable ID>
reference_contract: qualified-reference-v1
repository_identity: {scheme: github-repository-id-v1, authority: <GitHub host>, id: <numeric repository ID>}
plan_id: <PlanID>
authority_baseline_plan_ref: <exact prior accepted delegator PlanRef authorizing this grant>
delegator_role: <qualified role reference>
delegator_authority_source: <exact source locator at authority_baseline_plan_ref>
delegate_role: <qualified role reference>
parent_milestone: <qualified milestone reference or none>
activation_rule: <accepted publication of this grant and required valid delegate Role/binding>
supersedes: <prior delegation ID or none>
```

The authority baseline is not the unknown SHA of the commit that first contains this delegation. Its accepted containing relationship PlanRef is resolved from publication evidence afterward. For a new child, the intended delegate identity is bounded by the parent-authorized initialization; the child Role/binding must actually become accepted before it can act. See `planning/REFERENCES.md`.

The header's repository/PlanID identifies the delegation record, not both endpoints. Each cross-plan endpoint must be fully qualified; a same-plan endpoint may use a short RoleID only in that unambiguous context. At use, bind the delegate's accepted PlanRef and the delegator's current authority/relationship PlanRef separately. They need not equal each other or this grant's prior baseline. Naming both endpoints `ChildLead` does not make them the same Role.

## Delegated scope

State an exact subset of the delegator's existing scope.

## Delegated final decisions

List each final decision scope transferred to the delegate. Do not use open-ended phrases such as `normal decisions`, `as needed`, or `all technical matters` unless that exact scope is already formally defined elsewhere and linked.

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

`ACCEPT_CHILD_MILESTONES` permits the delegate to serve as an acceptance authority inside the delegated scope; it does not itself accept any milestone. Each milestone contract must still identify its acceptance authority, and each accepted milestone requires its own durable acceptance record.

## Explicit exclusions

List retained parent authority and prohibited scope.

## Escalation triggers

List conditions that must return to the delegator or higher parent authority.

## Acceptance responsibility

State which child milestones, if any, the delegate may accept and whether the delegator retains parent-milestone acceptance. Do not infer milestone acceptance from delivery responsibility or from possession of `ACCEPT_CHILD_MILESTONES` alone.

## Validity checks

Before accepting this delegation, verify:

- the delegator currently holds every authority being delegated;
- scope only narrows;
- no conflicting final authority is created;
- the delegate Role exists or is validly created under `CREATE_SUBROLES`;
- no repository/device/data/spending/release authority is implied unless explicitly possessed and delegated;
- the delegation does not manufacture reviewer independence.

A delegation cannot authorize its own creation. Its authority source must predate the delegation.
