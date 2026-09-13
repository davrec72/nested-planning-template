# Recursive nesting and delegation

This file defines how plans compose downward into child plans and upward into parent/super-project plans.

The rules are recursive and have no fixed depth limit.

## Core law

> **Authority may be delegated downward only as a subset of authority already held. A child plan is an implementation of a parent scope; it is not a new authority source.**

The parent owns the boundary contract. The child owns only the internal decomposition permitted by that contract.

## Required child-plan identity

Every active child plan using the current grammar must declare:

```text
plan_id: <stable PlanID>
grammar: plan-grammar-v2
parent_plan: <parent PlanID or external locator>
parent_plan_ref: <exact accepted parent PlanRef>
parent_milestone: <exact parent MilestoneID>
scope_owner_role: <exact RoleID>
parent_contract: <durable parent-facing contract path/link>
```

Missing or placeholder values make the child plan non-operational for substantive dispatch.

## Delegation capabilities

Delegation capabilities are opt-in. Absence means `not authorized`.

Supported capability IDs:

```text
DECOMPOSE_SCOPE
CREATE_SUBROLES
BIND_SUBROLE_HOLDERS
DELEGATE_DECISIONS
ACCEPT_CHILD_MILESTONES
```

### DECOMPOSE_SCOPE

Allows the Role to create and modify a child plan inside its already accepted parent scope.

Does not permit changing the parent milestone, parent dependencies, or parent acceptance contract.

### CREATE_SUBROLES

Allows creation of durable subordinate Roles whose scope is strictly inside the delegating Role's current scope.

Does not permit granting authority the delegating Role does not possess.

### BIND_SUBROLE_HOLDERS

Allows binding/unbinding holders to subordinate Roles created within delegated scope.

Does not permit rebinding parent/sibling Roles.

### DELEGATE_DECISIONS

Allows transferring a defined subset of the delegating Role's own final decision authority to a subordinate Role.

The delegated decision scope must be explicit. The parent Role cannot retain simultaneous final authority over exactly the same decision unless the accepted planning grammar defines a joint mechanism.

### ACCEPT_CHILD_MILESTONES

Allows final acceptance of child-plan milestones within the delegated scope.

Under `plan-grammar-v2`, possession of this capability does not itself accept any milestone. Each accepted child milestone still requires the milestone contract, authority source, and durable acceptance record required by `CONVENTIONS.md`.

This does not imply authority to accept the parent milestone. Parent acceptance remains with the parent-facing authority unless explicitly delegated.

## What a child plan may change autonomously

Only when its scope owner has the necessary capabilities, a child plan may change:

- internal milestones;
- internal gates and decisions;
- internal scheduling preferences;
- internal subordinate Role structure;
- internal work decomposition;
- internal sequencing;
- internal implementation choices;
- child milestone status based on authorized acceptance.

These changes are autonomous only when they do not alter the parent-facing contract.

## What a child plan may never change by itself

A child plan may not:

- broaden its parent scope;
- weaken or rewrite parent acceptance criteria;
- alter parent-level hard dependencies or scheduling semantics;
- change the identity of the parent milestone it implements;
- modify shared contracts explicitly owned by a parent or sibling scope;
- grant repository, device, data, financial, privacy, or release authority absent from the accepted delegation;
- appoint itself to a parent Role;
- manufacture reviewer independence by assigning several Roles to the same holder;
- change another child plan's authority;
- accept its own parent milestone unless that authority was explicitly delegated.

Any such proposal must escalate to the appropriate parent authority before execution.

## Parent accountability

Delegating execution does not erase responsibility for the parent-facing outcome.

A parent Role may rely on accepted child evidence instead of re-reviewing every implementation detail, but remains responsible for its own parent-level acceptance decision unless that decision authority was explicitly delegated.

## When to create a child plan

Create a durable child plan when at least one of these is true:

- the scope contains several meaningful parallel workstreams;
- the scope has its own nontrivial dependency graph;
- several durable decision scopes exist;
- the parent Role can no longer reasonably supervise all details;
- stable ownership boundaries would reduce coordination burden;
- the subsystem is large enough to benefit from its own at-a-glance roadmap.

Do not create a child plan merely because another temporary worker would help.

## When to create a subordinate Role

Create a durable subordinate Role only when stable authority/responsibility is needed.

Temporary implementers, reviewers, researchers, and test agents normally remain workers coordinated by Foreman and do not require durable RoleIDs.

They validate a bounded executor authorization under `EXECUTION.md`; they do not impersonate the serving Role or receive Role delegation capabilities through assignment.

## Internal path convention

For child plans inside the same repository, use:

```text
planning/plans/<PlanID>/PLAN.md
planning/plans/<PlanID>/ROLES.md
```

The child inherits `planning/CONVENTIONS.md` and this file. It must not create a competing local planning grammar unless a parent-authorized grammar fork is explicit.

## Cross-repository nesting

A parent plan may treat another repository as the implementation of one parent milestone.

Parent and child repositories keep independent Git histories.

### Parent-side record

The parent records at least:

```text
repository: <owner/repo>
plan_path: planning/PLAN.md
plan_id: <child PlanID>
scope_owner_role: <child boundary RoleID>
parent_contract: <path/link in parent repo>
```

For an actual dispatch, decision, or acceptance, bind an exact child commit SHA as the child's PlanRef.

### Child-side record

The child fills `planning/PARENT.md` with:

```text
parent_repository: <owner/repo>
parent_plan_path: <path>
parent_plan_id: <PlanID>
parent_plan_ref: <exact parent PlanRef>
parent_milestone: <MilestoneID>
parent_contract: <durable locator>
scope_owner_role: <RoleID>
```

### No submodule authority

Git submodules, forks, branch ancestry, repository ownership, copied files, or shared commit history do not create planning authority.

The authority relationship comes from accepted Role/delegation records plus the parent contract.

## Parent/child synchronization rule

The parent does **not** update for every internal child commit.

A parent plan update is required when any parent-visible boundary changes, including:

- child repository or PlanID identity;
- parent-facing milestone outcome or acceptance criteria;
- delegated authority;
- parent dependency/scheduling semantics;
- parent milestone status;
- parent contract version/meaning.

Internal child-plan changes that preserve the parent contract do not require a parent commit.

## Native vs. opaque child plans

Native interpretation requires a grammar version that the parent explicitly knows to be compatible.

For the current contract:

- a `plan-grammar-v2` parent may natively interpret a `plan-grammar-v2` child only for semantics it supports, including any explicitly declared Decision/DATA node-contract version under `NODE_CONTRACTS.md`; unsupported node contracts fail closed at the affected node/boundary rather than acquiring meaning from the shared grammar label;
- `plan-grammar-v1` and `plan-grammar-v2` are **not** silently compatible;
- a v1 child remains valid under its own historical v1 semantics, but a v2 parent must not reinterpret its internal Milestones, acceptance state, or dependency activation as though the child had produced v2 records;
- until a cross-version child is migrated or an explicit compatibility rule is accepted, treat the child boundary as **opaque**: rely only on the explicit parent contract and accepted boundary evidence.

A child using a different planning system or an incompatible grammar version is opaque for the semantics the parent cannot safely interpret. Agents must not silently translate foreign or older records into the current grammar.

### Migrating v1 child plans to v2

Migration is a forward planning transition, not a rewrite of history.

When migrating a child from `plan-grammar-v1` to `plan-grammar-v2`:

1. create an accepted v2 PlanRef that declares `grammar: plan-grammar-v2` and adopts the v2 milestone/acceptance lifecycle for future operation;
2. preserve historical v1 records and their original meaning;
3. do **not** fabricate or backdate v2 milestone-acceptance receipts merely to make historical v1 completions appear native to v2;
4. if a historical v1 completion must matter to current v2 reasoning, carry it forward through an explicit migration/current-state decision or re-establish the relevant current state under v2 evidence and authority; otherwise leave it outside native v2 milestone semantics;
5. update the parent/child compatibility record if the migration changes what the parent may interpret natively.

A v2 migration does not by itself broaden delegated scope, alter the parent contract, or grant new authority.

## Upward nesting

This repository may itself be one milestone in a larger super-project or portfolio plan.

Example:

```text
portfolio-plan
  P1: Robotics program
      child -> robot-plan
          R2: Learning system ready
              child -> learning-project
```

Each level sees the next level through a contract. Higher levels need not supervise internal child mechanics unless the boundary changes or an escalation condition is met.

## Escalation

Escalate upward when:

- a required capability is missing;
- child work would change a parent contract;
- two Roles appear to have conflicting final authority;
- cross-scope shared contracts must change;
- requested work exceeds delegated permissions/resources;
- a parent-facing milestone cannot be met under current constraints;
- accepted records are contradictory or materially stale.

Do not escalate routine internal implementation decisions that remain inside delegated scope.

## Foreman and nested work

Foreman is a shared execution-orchestration Role.

An authorized Lead may direct Foreman to coordinate work inside that Lead's scope. That does not grant the Lead authority over Foreman's unrelated queues and does not grant Foreman the Lead's substantive decision rights.

Every nested substantive work package must bind:

```text
plan_id=<PlanID>
plan_ref=<exact PlanRef>
role=<RoleID>
target_type=<milestone | decision | data | plan-maintenance>
target_id=<stable local node/scope ID>
target_record=<exact accepted definition>
parent_plan_ref=<exact parent PlanRef>
```

Foreman must refuse or escalate materially missing/contradictory bindings.

Include the complete package/authorization/attempt binding required by `EXECUTION.md` and the actual parent identity/Milestone/contract required above. A local Decision target does not invent a local Milestone or replace the real parent boundary.

## Nested plan change propagation

Child-plan changes notify Foreman event-first just like root-plan changes, but propagation is scoped.

Foreman sends the delta only to affected child Role holders/work packages. Parent plans are not churned by internal child edits unless the parent-facing boundary changes.

If the parent boundary changes, notify the parent Foreman/coordination route as required by that parent plan.

Use the durable per-recipient receipts, bounded execution checks, and recovery procedure in `EXECUTION.md`. An offline child or unacknowledged pause remains outstanding; sending the delta does not prove it stopped.

## Authority cycles are invalid

Delegation must be acyclic.

A Role may not receive authority downstream that eventually points back to itself through a delegation cycle.

If a cycle is discovered, all decisions that depend on the ambiguous cycle pause until the nearest valid parent authority resolves it.

## One holder, multiple Roles

One holder may occupy multiple Roles where shared context is useful.

Durable decisions must state which Role the holder is acting as.

Role multiplicity does not create independent review contexts.

## No fixed depth limit

Nested plans may recurse as deeply as useful. Depth is not a goal.

Create hierarchy only when it reduces cognitive load or coordination cost. If a child plan is smaller than the overhead needed to maintain its Role/contract structure, keep the work in the parent plan or ordinary work packages instead.
