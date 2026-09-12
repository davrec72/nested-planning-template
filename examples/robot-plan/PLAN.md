# Example: robot-plan parent roadmap

This is an example only. It demonstrates a parent repository treating another repository as one milestone.

```text
plan_id: ROBOT
grammar: plan-grammar-v2
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

## Child implementation binding for R2

```text
repository: example-owner/learning-project
plan_path: planning/PLAN.md
plan_id: LEARNING
scope_owner_role: LearningLead
parent_contract: examples/robot-plan/PARENT_CONTRACT.md
```

The parent does not need to mirror the child's internal milestones. It cares only whether R2's contract is met.
