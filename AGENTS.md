# AGENTS.md

This repository defines a planning and delegation system for AI-heavy projects. Read this file before making planning, delegation, dispatch, or acceptance decisions.

## Non-negotiable planning invariants

1. **Authority belongs to Roles, not holders.** A person, chat, model, account, or process may hold one or more Roles, but the Role is the authority-bearing object.
2. **A proposed plan edit cannot authorize its own approval.** Use authority that existed before the change.
3. **Delegation only narrows.** A child Role or child plan may receive only a subset of authority already held by the delegating Role.
4. **Parent contracts cannot be weakened from below.** Child plans own internal decomposition only; parent plans own parent-facing outcomes, acceptance criteria, parent-level dependencies, and delegated scope.
5. **Repository/tool access is not authority.** Write permission, seniority, chat history, prior behavior, or being the most informed agent never substitute for an accepted Role binding.
6. **Ambiguity means no authority.** If accepted records are missing, contradictory, ambiguous, stale in a material way, or only proposed in an unmerged change, stop the affected decision/dispatch and escalate.
7. **One final Role per substantive decision scope.** Advisers and reviewers may be many. Final authority for the same decision scope may not be simultaneously assigned to multiple Roles unless the planning grammar explicitly defines a joint mechanism.
8. **Role separation is not reviewer independence.** Two Roles held by the same underlying agent/context do not count as independent reviewers merely because their RoleIDs differ.
9. **Milestones are outcomes.** Do not use milestone nodes for activities such as `review X` unless completion of that activity is itself the intended outcome.
10. **Gates are predicates; Decisions are judgments.** Do not hide human/agent choice inside a Gate.
11. **Plan changes propagate by explicit notification plus boundary checks, not constant polling.**
12. **Exact accepted Git commits are PlanRefs.** Mutable branch names are locators only.

## Before any substantive planning or execution action

An AI must identify from accepted records:

- `plan_id`;
- exact `plan_ref`;
- acting `role`;
- current holder binding for that Role;
- milestone or decision scope;
- authority source for the action;
- if nested: parent plan, parent PlanRef, parent milestone, and parent contract;
- if delegating: the exact delegation capability that permits the action.

If any required item is unavailable or contradictory, do not infer it. Escalate to the nearest Role that has accepted authority over the disputed scope.

## Canonical files

Read these together:

- `planning/PLAN.md` — at-a-glance roadmap.
- `planning/CONVENTIONS.md` — exact node and edge grammar.
- `planning/ROLES.md` — current Role holders and authority/delegation capabilities.
- `planning/NESTING.md` — downward and upward nesting rules.
- `planning/PARENT.md` — parent relationship if this repository is itself nested.

## Creating or changing a plan

Use only the grammar in `planning/CONVENTIONS.md`.

A planning change must state:

```text
Semantic delta:
Affected milestones:
Affected roles:
Active work impact: none | continue | pause | redirect | supersede
Authority impact: none | binding change | scope change
Foreman dispatch required:
Controlling decision/evidence:
```

Do not add a new arrow label or node semantic without first changing the grammar.

## Creating child plans or subordinate Roles

Do not create them merely because another worker would be convenient.

A Role may create durable child planning structures only when its accepted Role record grants the required capability. The supported capability IDs are defined in `planning/NESTING.md`.

A child plan may reorganize internal work only inside its accepted parent contract. Any change to the parent-facing outcome, parent acceptance criteria, parent dependencies, shared contracts owned above the child, spending, repository permissions, device/data access, or scope must return to the appropriate parent authority.

## Foreman

`Foreman` is a shared execution-orchestration Role, not automatically a substantive technical decision-maker.

The Foreman holder MUST be an environment that can:

- delegate work to other agents/contexts; and
- schedule future follow-up tasks/checks.

A plain chat that cannot do both MUST NOT be bound to the Foreman Role.

Foreman coordinates authorized work packages, reviewer routing, status follow-up, and plan-change propagation. Foreman acquires no Lead authority merely by coordinating a Lead's work.

See `prompts/FOREMAN.md` for the complete Role prompt.

## Work packages

Every substantive work package must bind to accepted planning state using at least:

```text
plan_id=<PlanID>
plan_ref=<exact accepted commit SHA>
role=<RoleID>
milestone=<MilestoneID>
```

For nested work also include:

```text
parent_plan_ref=<exact parent PlanRef>
```

Foreman and executing agents must refuse or escalate materially contradictory bindings rather than silently choosing one.

## Cross-repository nesting

Repositories keep independent Git histories. Parent/child authority is established through explicit parent contracts, Role delegations, and exact PlanRefs.

Do not treat Git submodules, forks, copied trees, branch ancestry, or repository ownership as authority relationships.

## Domain-specific projects

Projects created from this template must add their own safety, privacy, release, data-integrity, hardware, legal, and technical invariants. This template does not override them.
