# Example parent contract for R2

```text
contract_id: ROBOT-R2-LEARNING-v1
parent_plan_id: ROBOT
parent_plan_ref: <example parent commit SHA>
parent_milestone: R2
child_repository: example-owner/learning-project
child_plan_id: LEARNING
child_plan_path: planning/PLAN.md
child_scope_owner_role: LearningLead
```

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
