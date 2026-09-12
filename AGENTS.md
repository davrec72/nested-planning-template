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
10. **Delivery, evidence, acceptance, and roadmap activation are separate facts.** Completing work or producing evidence does not itself accept a milestone. A durable acceptance record establishes the acceptance decision. When a Milestone is the source of a hard prerequisite, downstream dispatch opens only after an accepted projection PlanRef records that acceptance as current roadmap state (`MILESTONE_DONE` plus its acceptance-record index).
11. **A milestone contract may reference acceptance authority; it cannot create it.** Naming an `Acceptance authority` Role or an `Acceptance authority source` in the milestone record does not grant that authority. The cited authority source must be independently accepted and must actually cover that milestone/scope; otherwise acceptance authority is absent.
12. **Issued acceptance records are immutable history.** Do not edit or reinterpret an issued acceptance in place. Corrections/replacements create new durable records; later invalidation/revocation is a separate durable decision and accepted plan change, not a rewrite of the old receipt.
13. **Grammar versions are semantic contracts.** Read the declared `grammar` before interpreting a plan. Do not silently apply `plan-grammar-v2` milestone/activation semantics to v1 or otherwise incompatible plans. Follow `planning/NESTING.md` for cross-version child boundaries and migration.
14. **Gates are predicates; Decisions are judgments.** Do not hide human/agent choice inside a Gate.
15. **Plan changes propagate by explicit notification plus boundary checks, not constant polling.**
16. **Exact accepted Git commits are PlanRefs.** Mutable branch names are locators only.
17. **Current planning state comes from a valid publication record, not from branch freshness.** In an instantiated project, resolve `planning/CURRENT.md` under `planning/PUBLICATION.md`; the exact `plan_ref` named by the latest valid publication is the current accepted PlanRef. A newer default-branch commit may contain staged/unpublished planning content and must not silently become operative.
18. **Root bootstrap is a one-time external exception.** A root project with no parent may use an explicitly designated external Founding Authority only to establish its first accepted authority state under `planning/PUBLICATION.md`. After the first valid publication, ordinary Role-based authority rules apply; repository ownership/write access never substitutes for the founding trust anchor.

## Before any substantive planning or execution action

An AI must identify from accepted records:

- `plan_id`;
- declared `grammar`;
- current `publication_id`;
- exact current `plan_ref` obtained from a valid `planning/CURRENT.md` publication;
- acting `role`;
- current holder binding for that Role;
- milestone or decision scope;
- authority source for the action;
- if accepting a milestone: the exact `contract_plan_ref`, the accepting Role, an independently accepted authority source covering that milestone/scope, and the evidence being accepted;
- if dispatch depends on a completed milestone: the current accepted projection PlanRef must actually project that milestone as `MILESTONE_DONE` and index its acceptance record;
- if nested: parent plan, parent PlanRef, parent milestone, parent contract, and child/parent grammar compatibility;
- if delegating: the exact delegation capability that permits the action.

Do not use the default-branch head as a substitute for `planning/CURRENT.md`.

If an instantiated project has no valid `planning/CURRENT.md`, ordinary substantive project execution is not initialized under this protocol. Only the bounded root/parent bootstrap actions defined in `planning/PUBLICATION.md` may proceed.

If any required item is unavailable or contradictory, do not infer it. Escalate to the nearest Role that has accepted authority over the disputed scope, or to the designated Founding/parent authority during valid bootstrap.

If a nested plan declares an incompatible grammar, do not natively interpret its internal milestone/status semantics. Use the boundary rules in `planning/NESTING.md`.

## Canonical files

Read these together:

- `planning/PLAN.md` — at-a-glance roadmap.
- `planning/CONVENTIONS.md` — exact node and edge grammar.
- `planning/NESTING.md` — downward and upward nesting rules.
- `planning/ROLES.md` — Role scopes, holders, and delegation capabilities.
- `planning/PUBLICATION.md` — root bootstrap and current-PlanRef publication protocol.
- `planning/CURRENT.md` — required in an instantiated project; authoritative locator/index for the current accepted PlanRef.
- `planning/FOUNDING.md` — required for a root-project bootstrap; historical after the first publication.
- `planning/PARENT.md` — parent relationship if this repository is itself nested.

The template source may contain templates instead of an instantiated `CURRENT`/`FOUNDING` record. A copied/forked project becomes operational only after those records are instantiated as required by `planning/PUBLICATION.md`.

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

A semantic plan/Role change does not become current merely because its commit or PR is merged. Publish the exact resulting candidate under `planning/PUBLICATION.md`. Foreman propagation begins only after a valid publication makes that candidate the current accepted PlanRef.

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

Foreman MUST discover the current accepted PlanRef through `planning/CURRENT.md` / `planning/PUBLICATION.md`, not by choosing the newest branch or commit.

See `prompts/FOREMAN.md` for the complete Role prompt.

## Work packages

Every substantive work package must bind to accepted planning state using at least:

```text
plan_id=<PlanID>
plan_ref=<exact current accepted commit SHA from planning/CURRENT.md>
role=<RoleID>
milestone=<MilestoneID>
```

For nested work also include:

```text
parent_plan_ref=<exact parent PlanRef>
```

Foreman and executing agents must refuse or escalate materially contradictory bindings rather than silently choosing one.

Work-package completion may return evidence for a milestone but does not itself accept that milestone. Milestone acceptance must be recorded separately by a Role whose acceptance authority is established independently of the milestone contract; use `templates/MILESTONE_ACCEPTANCE.md`.

The acceptance record binds the exact pre-acceptance `contract_plan_ref`. A later plan commit that projects `MILESTONE_DONE` or indexes the acceptance record is a different PlanRef and does not retroactively become the contract revision that was judged.

An acceptance record may exist before that projection commit, but it does not by itself authorize Foreman to treat a downstream **Milestone-source** hard prerequisite as open. Operational dispatch follows the current accepted PlanRef. Only after the accepted projection is published as current and records `MILESTONE_DONE` plus the acceptance index may that Milestone prerequisite be treated as satisfied for dispatch.

Do not mutate an issued acceptance record to reflect later planning state. Preserve it as history; record later correction/revocation/reopening separately and propagate the resulting current state through an accepted and published plan change.

## Cross-repository nesting

Repositories keep independent Git histories. Parent/child authority is established through explicit parent contracts, Role delegations, exact PlanRefs, and each repository's valid publication state.

Do not treat Git submodules, forks, copied trees, branch ancestry, or repository ownership as authority relationships.

A child repository's first accepted internal state may be bootstrapped from an accepted parent contract under `planning/PUBLICATION.md`; it does not need an unrelated root Founding Authority.

## Domain-specific projects

Projects created from this template must add their own safety, privacy, release, data-integrity, hardware, legal, and technical invariants. This template does not override them.
