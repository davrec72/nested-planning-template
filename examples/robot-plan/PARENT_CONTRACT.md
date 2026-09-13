# Example parent contract for R2

The repository IDs 1001/1002 and readable names are fictional examples, not verified live bindings. Operational adoption requires accepted publication and verified provider identities under `planning/REFERENCES.md`.

```text
contract_id: ROBOT-R2-LEARNING-v1
reference_contract: qualified-reference-v1
parent_plan: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}, "plan_id": "ROBOT", "object_kind": "plan"}
authority_baseline_plan_ref: <P0: exact prior accepted parent SHA authorizing creation>
parent_authority_role: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}, "plan_id": "ROBOT", "object_kind": "role", "object_id": "ProgramLead"}
parent_authority_source: <exact pre-existing authority source at P0>
parent_milestone: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}, "plan_id": "ROBOT", "object_kind": "milestone", "object_id": "R2"}
child_plan: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1002"}, "plan_id": "LEARNING", "object_kind": "plan"}
child_repository_locator: example-owner/learning-project
child_plan_path: planning/PLAN.md
child_scope_owner_role: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1002"}, "plan_id": "LEARNING", "object_kind": "role", "object_id": "LearningLead"}
```

This is an illustrative contract, not live authority. The later exact accepted parent relationship revision P1 contains this contract citing P0; the child pins P1. Do not replace P0 with P1 inside this new contract or require it to contain its own SHA. See `planning/REFERENCES.md` for same-repository and cross-repository sequences.

## Required outcome

The child learning project provides a versioned learning subsystem that can be integrated with the robot program through the agreed boundary.

## Acceptance criteria

- a documented interface is available to the parent integration work;
- required artifacts are versioned and reproducible;
- parent integration constraints are met;
- child evidence identifies the exact accepted child PlanRef/revision;
- unresolved child limitations relevant to robot integration are explicit.

## Delegated scope

The child may design, implement, test, and internally reorganize its learning subsystem inside this outcome.

## Explicit exclusions

The child may not independently:

- alter robot hardware requirements;
- change robot-system safety policy;
- redefine R2 acceptance criteria;
- modify sibling project scopes;
- commit parent spending/resources not already delegated.

## Delegation capabilities

```text
DECOMPOSE_SCOPE
CREATE_SUBROLES
BIND_SUBROLE_HOLDERS
DELEGATE_DECISIONS
ACCEPT_CHILD_MILESTONES
```

These capabilities apply only inside the delegated learning-project scope.

## Parent acceptance authority

```text
parent_acceptance_role: RobotProgramLead
```

## Escalation triggers

Escalate when the child needs a parent contract change, robot hardware/safety change, additional unapproved resources, or a cross-project architectural decision.
