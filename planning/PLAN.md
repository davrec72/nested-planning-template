# Project plan

```text
plan_id: <replace-with-stable-PlanID>
grammar: plan-grammar-v1
```

This file is the canonical at-a-glance roadmap for the project. Replace all angle-bracket placeholders before treating it as operational.

Interpret this diagram only under `CONVENTIONS.md`. Current holder/authority bindings are in `ROLES.md`. Parent scope, if any, is in `PARENT.md`.

```mermaid
flowchart TD

  %% PLAN GRAMMAR v1
  %% A --> B                         hard prerequisite
  %% A -. "preferred before" .-> B  scheduling preference only
  %% ROLE -- "assigned to" --> MILESTONE
  %% ROLE -- "decides" --> DECISION
  %% ordinary multiple hard inputs = AND
  %% OR / N-of-M requires an explicit GATE
  %% milestone status is expressed only by class

  %% ROLES
  ProjectLead["Project Lead"]
  SubsystemLead["Subsystem Lead"]
  class ProjectLead,SubsystemLead ROLE

  %% MILESTONES / GATES / DECISIONS
  M1["M1: First foundation validated"]
  M2["M2: Second foundation validated"]
  G1{"At least 2 validated"}
  D1{"Select integration strategy"}
  M3["M3: Integrated system validated"]

  M1 --> G1
  M2 --> G1
  G1 --> D1
  ProjectLead -- "decides" --> D1
  D1 -- "integrate" --> M3

  ProjectLead -- "assigned to" --> M1
  SubsystemLead -- "assigned to" --> M2
  ProjectLead -- "assigned to" --> M3

  %% VISUAL LANGUAGE
  classDef ROLE fill:whitesmoke,stroke:slategray,stroke-width:15px,color:black,font-weight:600,font-size:16px,rx:8,ry:8;
  classDef GATE fill:aliceblue,stroke:deepskyblue,stroke-width:1.5px,color:navy,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DECISION fill:lightyellow,stroke:darkorange,stroke-width:1.5px,color:darkgoldenrod,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DATA fill:mistyrose,stroke:red,stroke-width:1.5px,color:darkred,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef MILESTONE_DONE fill:honeydew,stroke:forestgreen,stroke-width:1.5px,color:darkgreen,font-weight:900,font-size:14px,rx:8,ry:8;
  classDef MILESTONE_INPROGRESS fill:lavender,stroke:purple,stroke-width:1.8px,color:indigo,font-weight:700,font-size:14px,rx:10,ry:10;
  classDef MILESTONE_PENDING fill:gainsboro,stroke:dimgray,stroke-width:1.5px,color:black,font-weight:600,font-size:14px,rx:8,ry:8;

  class G1 GATE
  class D1 DECISION
  class M1 MILESTONE_INPROGRESS
  class M2,M3 MILESTONE_PENDING

  linkStyle default stroke:slategray,stroke-width:3.5px,fill:none;
```

## Milestone contracts

For each milestone, maintain a durable record containing at least:

```text
MilestoneID:
Outcome:
Acceptance criteria:
Primary assigned Role:
Assignment authority source:
Acceptance authority:
Acceptance authority source:
Evidence location:
Acceptance record index: none | <durable locator>
Child plan: none | <internal path> | <external repository locator>
```

The primary assigned Role is responsible for delivery; it is not automatically the accepting authority. The same Role may perform both functions only when an independently accepted authority source explicitly grants both scopes.

The milestone's `Acceptance authority` field only references authority; it does not create it. If the named Role lacks an independently accepted authority source covering this milestone/scope, acceptance authority is absent.

`Acceptance record index` is projection/index metadata. In the exact pre-acceptance `contract_plan_ref` it will normally be `none`. After a durable acceptance record exists, a later status/index update may populate the locator and mark the node `MILESTONE_DONE`; that later commit has a different PlanRef and does not become the contract revision that was accepted.

`MILESTONE_DONE` is a roadmap projection of a durable milestone acceptance record. The class does not itself create acceptance. Use `templates/MILESTONE_ACCEPTANCE.md` for the acceptance record.

The Mermaid overview should remain terse. Put detailed acceptance criteria, evidence, and acceptance records in durable records rather than inside nodes.
