# Example: robot-plan parent roadmap

This is an example only. It demonstrates a parent repository treating another repository as one milestone.

The repository IDs 1001/1002 and readable names are fictional examples, not verified live bindings. Operational adoption requires accepted publication and verified provider identities under `planning/REFERENCES.md`.

```text
plan_id: ROBOT
grammar: plan-grammar-v2
reference_contract: qualified-reference-v1
repository_identity: {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}
repository_locator: example-owner/robot-plan
```

```mermaid
flowchart TD
  ProgramLead["Robot Program Lead"]
  HardwareLead["Hardware Lead"]
  LearningLead["Learning-System Boundary Lead"]
  class ProgramLead,HardwareLead,LearningLead ROLE

  R1["R1: Robot hardware foundation validated"]
  R2["R2: Learning subsystem ready for robot integration"]
  R3["R3: Integrated robot behavior validated"]

  R1 --> R3
  R2 --> R3

  HardwareLead -- "assigned to" --> R1
  LearningLead -- "assigned to" --> R2
  ProgramLead -- "assigned to" --> R3

  classDef ROLE fill:whitesmoke,stroke:slategray,stroke-width:15px,color:black,font-weight:600,font-size:16px,rx:8,ry:8;
  classDef GATE fill:aliceblue,stroke:deepskyblue,stroke-width:1.5px,color:navy,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DECISION fill:lightyellow,stroke:darkorange,stroke-width:1.5px,color:darkgoldenrod,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DATA fill:mistyrose,stroke:red,stroke-width:1.5px,color:darkred,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef MILESTONE_DONE fill:honeydew,stroke:forestgreen,stroke-width:1.5px,color:darkgreen,font-weight:900,font-size:14px,rx:8,ry:8;
  classDef MILESTONE_INPROGRESS fill:lavender,stroke:purple,stroke-width:1.8px,color:indigo,font-weight:700,font-size:14px,rx:10,ry:10;
  classDef MILESTONE_PENDING fill:gainsboro,stroke:dimgray,stroke-width:1.5px,color:black,font-weight:600,font-size:14px,rx:8,ry:8;

  class R1,R2,R3 MILESTONE_PENDING
  linkStyle default stroke:slategray,stroke-width:3.5px,fill:none;
```

## Navigation

| Node | Relation | Go to |
|---|---|---|
| R2 | child plan | [Child plan (unresolved external placeholder)](https://<host>/example-owner/learning-project/blob/<navigation-ref>/planning/PLAN.md) |

This canonical target matches R2's `Child plan` below and the fictional external child repository/path. It is unresolved and nonoperational: fill the host and navigation ref with the actual child `PLAN.md` locator before use, then derive the table link from that source. See [external navigation](../navigation/README.md#external-child).

Source-tree documentation mirror only: [child example page](../child-project/PLAN.md). This local copy is not R2's canonical external child-plan target.

## Child implementation binding for R2

Navigation excerpt of the Milestone record (other contract semantics remain in the parent contract):

```text
MilestoneID: R2
Child plan: https://<host>/example-owner/learning-project/blob/<navigation-ref>/planning/PLAN.md
```

```text
child_plan: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1002"}, "plan_id": "LEARNING", "object_kind": "plan"}
repository_locator: example-owner/learning-project
plan_path: planning/PLAN.md
scope_owner_role: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1002"}, "plan_id": "LEARNING", "object_kind": "role", "object_id": "LearningLead"}
parent_contract: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}, "plan_id": "ROBOT", "object_kind": "contract", "object_id": "ROBOT-R2-LEARNING-v1"}
parent_contract_locator: examples/robot-plan/PARENT_CONTRACT.md
```

The parent does not need to mirror the child's internal milestones. It cares only whether R2's contract is met.

The local parent `LearningLead` node and the child boundary `LearningLead` Role are distinct qualified objects (ROBOT/1001 versus LEARNING/1002). The matching human name does not transfer authority.
