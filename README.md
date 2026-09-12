# Nested Planning Template

A repository-native planning system for AI-heavy projects that need clear authority, recursive delegation, visual roadmaps, and low-overhead execution coordination.

The system is designed so a project can be understood at a glance at one level, while allowing any sufficiently large milestone to become its own nested plan. The same mechanism also works upward: an entire repository can be one child milestone in a larger portfolio or super-project plan.

The core idea is simple:

> **Plans describe outcomes and dependencies. Roles hold authority. Holders temporarily occupy roles. Delegation can narrow authority downward, but never widen it. Parent plans own contracts; child plans own implementation inside those contracts.**

This repository is intentionally documentation-first. It does not require a planning service, database, workflow engine, or custom bot.

## What this solves

Use this template when you want to avoid common failure modes in AI-managed projects:

- chats or agents silently acquiring authority because they happen to have context;
- plans becoming prose that different agents interpret differently;
- top-level diagrams becoming unreadable as detail grows;
- subordinate leads creating incompatible planning conventions;
- a parent project needing to supervise every internal child-plan edit;
- plan changes failing to reach active workers;
- agents continuously polling for changes instead of receiving targeted updates;
- role names being confused with the person/chat currently holding them;
- multiple roles held by one agent being mistaken for independent review;
- child plans changing parent requirements or permissions without authorization.

## Repository layout

```text
AGENTS.md
README.md
planning/
  PLAN.md
  CONVENTIONS.md
  NESTING.md
  ROLES.md
  PARENT.md
prompts/
  FOREMAN.md
templates/
  PLAN.md
  ROLES.md
  CHILD_PLAN.md
  CHILD_ROLES.md
  WORK_PACKAGE.md
  PLAN_CHANGE.md
  PARENT_CONTRACT.md
  MILESTONE_ACCEPTANCE.md
examples/
  robot-plan/
    PLAN.md
    PARENT_CONTRACT.md
  child-project/
    PLAN.md
    PARENT.md
```

`planning/PLAN.md` is the at-a-glance roadmap. `planning/CONVENTIONS.md` defines the exact planning grammar. `planning/NESTING.md` defines recursive delegation. `planning/ROLES.md` records role holders and authority. `planning/PARENT.md` is used only when this repository itself is nested under another plan.

## Current grammar version

The current contract is **`plan-grammar-v2`**.

v2 makes milestone delivery/evidence, milestone acceptance, and the roadmap projection of that acceptance separate facts. A milestone-source hard prerequisite becomes operational only when the current accepted PlanRef projects the milestone `MILESTONE_DONE` and indexes its durable acceptance record.

`plan-grammar-v1` remains a valid historical contract. Do not silently reinterpret v1 plans as v2. Cross-version child plans are treated according to `planning/NESTING.md`; absent an explicit compatibility rule, a v2 parent treats an unmigrated v1 child's internals as opaque and relies on the parent-facing boundary contract/evidence.

## Required concepts

### Role

A **Role** is a stable authority/responsibility slot. It is not a person, chat, model, account, or process.

A holder can occupy multiple roles. Rebinding a role to another holder does not change the role's scope. Two roles held by the same underlying agent do not create reviewer independence.

### Milestone

A **Milestone** is an outcome with acceptance criteria. Milestone labels describe what becomes true, not an activity such as `review X` or `work on Y`.

### Gate

A **Gate** is an objective predicate. No role decides a gate.

Examples:

- `At least 2 source foundations validated`
- `All required checks passed`

### Decision

A **Decision** requires judgment. Every Decision has exactly one role with a `decides` edge.

### PlanRef

A **PlanRef** is the exact accepted Git commit SHA containing the planning state used by a work package or decision. Mutable branch names such as `main` are locators, not authority evidence.

## Mermaid grammar at a glance

```mermaid
flowchart TD

  %% PLAN GRAMMAR v2
  %% A --> B                        hard prerequisite
  %% A -. "preferred before" .-> B scheduling preference only
  %% ROLE -- "assigned to" --> MILESTONE
  %% ROLE -- "decides" --> DECISION
  %% ordinary multiple hard inputs = AND
  %% OR / N-of-M requires an explicit GATE
  %% milestone status is expressed only by class

  ProjectLead["Project Lead"]
  FeatureLead["Feature Lead"]
  class ProjectLead,FeatureLead ROLE

  M1["M1: Stable foundation"]
  M2["M2: Second subsystem validated"]
  TWO{"At least 2 validated"}
  D1{"Select integration strategy"}
  M3["M3: Integrated system validated"]

  M1 --> TWO
  M2 --> TWO
  TWO --> D1
  ProjectLead -- "decides" --> D1
  D1 -- "integrate" --> M3

  FeatureLead -- "assigned to" --> M2
  ProjectLead -- "assigned to" --> M3

  classDef ROLE fill:whitesmoke,stroke:slategray,stroke-width:15px,color:black,font-weight:600,font-size:16px,rx:8,ry:8;
  classDef GATE fill:aliceblue,stroke:deepskyblue,stroke-width:1.5px,color:navy,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DECISION fill:lightyellow,stroke:darkorange,stroke-width:1.5px,color:darkgoldenrod,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef DATA fill:mistyrose,stroke:red,stroke-width:1.5px,color:darkred,font-weight:700,font-size:14px,rx:12,ry:12;
  classDef MILESTONE_DONE fill:honeydew,stroke:forestgreen,stroke-width:1.5px,color:darkgreen,font-weight:900,font-size:14px,rx:8,ry:8;
  classDef MILESTONE_INPROGRESS fill:lavender,stroke:purple,stroke-width:1.8px,color:indigo,font-weight:700,font-size:14px,rx:10,ry:10;
  classDef MILESTONE_PENDING fill:gainsboro,stroke:dimgray,stroke-width:1.5px,color:black,font-weight:600,font-size:14px,rx:8,ry:8;

  class TWO GATE
  class D1 DECISION
  class M1 MILESTONE_INPROGRESS
  class M2,M3 MILESTONE_PENDING

  linkStyle default stroke:slategray,stroke-width:3.5px,fill:none;
```

Do not invent new arrow meanings casually. If the grammar needs a new relationship, change `planning/CONVENTIONS.md` first.

## Downward nesting

A lead may create a child plan only when its accepted role authority explicitly grants the required delegation capability.

Example:

```text
Top-level plan
  M1B: Glasses foundation
      child plan: GLASSES
        G1: Vendor connection validated
        G2: Durable capture validated
        G3: Diagnostics validated
        G4: Integrated glasses foundation accepted
```

The parent plan continues to show only `M1B`. The child plan contains the detailed graph.

The child may change its internal decomposition without changing the parent plan **only if the parent-facing contract is unchanged**.

A child may never use its own plan to:

- broaden its scope;
- weaken the parent milestone's acceptance criteria;
- alter parent-level dependencies;
- grant itself repository/device/data/spending authority;
- modify shared contracts owned above it;
- assign itself authority the parent never delegated.

See `planning/NESTING.md`.

## Upward nesting and multiple repositories

The same rules work upward.

A repository such as `robot-plan` can treat another repository as one child milestone:

```text
robot-plan
  R1: Robot hardware foundation
  R2: Learning subsystem ready
      child implementation -> another repository
  R3: Integrated robot validation
```

The parent repository stores a **parent contract** describing what the child must provide. The child repository stores `planning/PARENT.md` pointing back to the exact parent plan and milestone.

The repositories keep independent Git histories. Do not use Git submodules, copied source trees, or branch ancestry as the authority mechanism.

The parent normally changes only when the child boundary changes: child identity, parent-facing outcome, delegated authority, parent scheduling/dependency semantics, or parent milestone status. Internal child-plan edits do not require parent commits.

## The Foreman role

`Foreman` is the shared execution-orchestration role. It is not automatically the technical authority for the work it coordinates.

The Foreman holder **must** be a chat/agent environment capable of both:

1. delegating work to other agents/contexts; and
2. scheduling its own future follow-up tasks or checks.

Examples include ChatGPT Work-style conversations or another environment with equivalent delegation and scheduling capabilities.

Do **not** bind a plain chat that cannot schedule future work to the Foreman role. It may act as a worker or lead, but it cannot satisfy the Foreman contract.

Foreman uses scheduled follow-ups for work that depends on time or asynchronous external state, such as CI completion, independent review returns, release windows, or later checkpoints. Foreman does not continuously poll the plan. Plan propagation is event-driven with boundary checks.

The complete operating prompt is in `prompts/FOREMAN.md`.

## How plan changes propagate

Use **event-driven notification plus boundary checks**.

When a semantic plan or role change merges:

1. the merger/authorized planner identifies the new PlanRef;
2. Foreman receives the PlanRef, semantic delta, affected roles/milestones, authority impact, and active-work impact;
3. Foreman reads that exact revision;
4. Foreman routes only the relevant delta to affected role holders/work packages;
5. unaffected work continues;
6. new or materially revised work packages bind the current PlanRef.

Foreman also checks planning state before:

- dispatching new substantive work;
- materially resuming paused work;
- final readiness/merge/acceptance handoffs whose validity depends on the plan.

Role holders do not need timer-driven polling.

## When to create a child plan

Create durable nesting only when it reduces complexity. Good reasons include:

- several meaningful parallel workstreams;
- multiple durable decision scopes;
- supervision burden too large for one lead;
- a milestone with its own nontrivial dependency graph;
- a stable subsystem that needs its own roadmap.

Do not create a durable role or child plan merely because another worker is useful. Temporary workers are cheap; durable authority structures should remain sparse.

## How to start a project from this template

1. Copy or fork this repository.
2. Replace `planning/PLAN.md` with your project roadmap using only the defined grammar.
3. Define roles and holders in `planning/ROLES.md`.
4. Decide whether the repository is a root plan or a child. If it is a child, fill `planning/PARENT.md`.
5. Bind a qualified Foreman holder if the project will use autonomous execution coordination.
6. Record PlanRefs in substantive work packages.
7. Use `templates/PLAN_CHANGE.md` for semantic plan changes.
8. Add child plans only when a delegated role has the required capability.

## Authority rule that overrides convenience

A planning file is not a magic permission source.

A proposed edit cannot authorize its own approval. A child plan cannot create powers that the parent did not grant. Repository write access, seniority, chat history, tool availability, or being the most informed agent are not substitutes for accepted role authority.

When accepted records are missing, contradictory, ambiguous, or only proposed in an unmerged PR, treat authority as absent and escalate.

## Scope of this template

This template defines planning and delegation mechanics. It does not prescribe:

- a software-development methodology;
- a particular review count;
- a release process;
- a budgeting system;
- a specific AI provider;
- a requirement that every project use nested plans.

Projects should add domain-specific safety, data, release, legal, and technical invariants in their own `AGENTS.md` and durable contracts.
