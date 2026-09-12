# Child plan template

Fill every header field before substantive dispatch.

```text
plan_id: <stable PlanID>
grammar: plan-grammar-v1
parent_plan: <parent PlanID or external locator>
parent_plan_ref: <exact accepted parent PlanRef>
parent_milestone: <exact parent MilestoneID>
scope_owner_role: <exact RoleID>
parent_contract: <durable path/link>
```

This child plan implements the parent milestone. It does not redefine it.

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

  ChildLead["Child Lead"]
  SpecialistLead["Specialist Lead"]
  class ChildLead,SpecialistLead ROLE

  C1["C1: First child outcome validated"]
  C2["C2: Second child outcome validated"]
  C3["C3: Parent-facing child outcome ready"]

  C1 --> C3
  C2 --> C3

  ChildLead -- "assigned to" --> C1
  SpecialistLead -- "assigned to" --> C2
  ChildLead -- "assigned to" --> C3

  classDef ROLE fill:whitesmoke,stroke:slategray,stroke-width:15px,color:black,font-weight:600,font-size:16px,rx:8,ry:8;
  classDef GATE fill:aliceblue,stroke:deepskyblue,stroke-width:1.5px,color:navy,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DECISION fill:lightyellow,stroke:darkorange,stroke-width:1.5px,color:darkgoldenrod,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DATA fill:mistyrose,stroke:red,stroke-width:1.5px,color:darkred,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef MILESTONE_DONE fill:honeydew,stroke:forestgreen,stroke-width:1.5px,color:darkgreen,font-weight:900,font-size:14px,rx:8,ry:8;
  classDef MILESTONE_INPROGRESS fill:lavender,stroke:purple,stroke-width:1.8px,color:indigo,font-weight:700,font-size:14px,rx:10,ry:10;
  classDef MILESTONE_PENDING fill:gainsboro,stroke:dimgray,stroke-width:1.5px,color:black,font-weight:600,font-size:14px,rx:8,ry:8;

  class C1 MILESTONE_INPROGRESS
  class C2,C3 MILESTONE_PENDING

  linkStyle default stroke:slategray,stroke-width:3.5px,fill:none;
```

## Parent-facing invariant

Internal child changes are allowed only when all of these remain unchanged:

```text
parent milestone identity
parent required outcome
parent acceptance criteria
parent dependencies/scheduling semantics
delegated authority boundary
shared contracts owned above this child
```

If any item must change, stop treating the change as internal and escalate to the parent authority.

## Child milestone records

For each child milestone maintain:

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
```

Assignment is responsibility for delivery, not implicit authority to accept the delivered outcome. Naming an `Acceptance authority` Role does not grant that authority; the cited authority source must be independently accepted and cover the child milestone/scope.

The pre-acceptance `contract_plan_ref` normally has `Acceptance record index: none`. After a durable acceptance record exists, a later child-plan status/index commit may populate the locator and project `MILESTONE_DONE`. That later PlanRef is not the contract revision judged by the acceptance record.

Use `templates/MILESTONE_ACCEPTANCE.md` for durable child milestone acceptance.
