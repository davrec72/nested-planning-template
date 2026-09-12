# AGENTS.md

This repository defines a planning and delegation system for AI-heavy projects. Read this file before making planning, delegation, dispatch, or acceptance decisions.

## Non-negotiable planning invariants

1. **Authority belongs to Roles, not holders.** A person, chat, model, account, or process may hold one or more Roles, but the Role is the authority-bearing object.
2. **A proposed plan edit cannot authorize its own approval.** Use authority and governance that existed before the change.
3. **Delegation only narrows.** A child Role or child plan may receive only authority already held by the delegating Role.
4. **Parent contracts cannot be weakened from below.** Child plans own internal decomposition only; parent plans own parent-facing outcomes, acceptance criteria, parent dependencies, and delegated scope.
5. **Repository/tool access is not authority.** Write permission, seniority, context, prompt reach, or being the most informed agent never substitute for accepted authority.
6. **Ambiguity means no authority.** If accepted records are missing, contradictory, materially stale, or merely proposed, stop the affected action and escalate.
7. **One final Role per substantive decision scope.** Advisers/reviewers may be many; final authority for one scope may not be simultaneously assigned unless an explicit joint mechanism exists.
8. **Role separation is not reviewer independence.** Two Roles held by the same underlying context do not create independent review.
9. **Milestones are outcomes.** Do not use Milestone nodes for activities unless completion of that activity is itself the outcome.
10. **Delivery, evidence, acceptance, and roadmap activation are separate facts.** Work/evidence does not itself accept a Milestone. A Milestone-source prerequisite opens only when the current accepted PlanRef projects DONE and indexes valid acceptance.
11. **A Milestone contract may reference acceptance authority; it cannot create it.** The authority source must independently grant that scope.
12. **Issued acceptance records are immutable history.** Corrections/revocations/reopenings are later records and plan changes, not in-place rewrites.
13. **Grammar versions are semantic contracts.** Do not silently reinterpret incompatible versions.
14. **Gates are predicates; Decisions are judgments.** Do not hide judgment in a Gate.
15. **Plan changes propagate by explicit notification plus boundary checks, not constant polling.** Notification is a wake mechanism, not authority.
16. **Exact accepted Git commits are PlanRefs.** Mutable branches are locators only.
17. **Current planning state is established by validated publication history.** An instantiated project uses the configured publication ref (portable default `refs/heads/plan-publications`) and `planning/CURRENT.md` carrier history under `planning/PUBLICATION.md` plus `planning/PUBLICATION_TRANSITIONS.md`. Default-branch freshness is not acceptance.
18. **The predecessor accepted rules validate the next publication transition.** Unpublished candidate changes to AGENTS/PUBLICATION cannot govern the transition that makes themselves current. Once accepted, they may govern later transitions.
19. **Publication history is serialized.** Each publication carrier after the first must descend directly from the actual incumbent carrier, and the publication ref must advance non-force from that exact predecessor. A self-reported predecessor field is not enough.
20. **Root bootstrap is one bounded external exception.** A root project may use an explicitly designated external Founding Authority only to establish its first accepted state. After first publication, ordinary Role/governance rules apply.

## Before any substantive planning or execution action

Resolve from accepted records:

- project/plan identity;
- configured publication ref;
- validated `publication_commit`, `publication_id`, and current `plan_ref`;
- declared grammar;
- acting Role and current holder binding;
- target Milestone/Decision/scope;
- authority source;
- when accepting a Milestone: exact `contract_plan_ref`, accepting Role, authority source, and evidence;
- when dispatch depends on DONE: the current PlanRef must actually project DONE and index acceptance;
- when nested: parent plan/ref/milestone/contract and grammar compatibility;
- when delegating: exact delegation capability.

For publication discovery, do not read governance from an unpublished default-branch candidate and use it to validate incumbent state. Follow `planning/PUBLICATION_TRANSITIONS.md`.

If publication history is absent/invalid, ordinary execution is not initialized. Only the bounded root/parent bootstrap actions defined by the publication protocol may proceed.

## Canonical files

Read together as applicable:

- `planning/PLAN.md` — roadmap.
- `planning/CONVENTIONS.md` — node/edge grammar.
- `planning/NESTING.md` — recursive delegation.
- `planning/ROLES.md` — Role scopes/holders/capabilities.
- `planning/PUBLICATION.md` — bootstrap and publication model.
- `planning/PUBLICATION_TRANSITIONS.md` — normative validator source, serialized carrier history, recovery, and notification matching.
- `planning/CURRENT.md` — instantiated publication record carried on the publication ref.
- `planning/FOUNDING.md` — root founding record when applicable.
- `planning/PARENT.md` — parent relationship when nested.

The template source may ship templates rather than an instantiated operational plan.

## Creating or changing a plan

Use only the accepted grammar. State semantic delta, affected milestones/Roles, active-work impact, authority impact, Foreman dispatch requirement, and controlling evidence/decision.

A semantic candidate does not become current merely because it exists or merges. Approval binds the exact candidate. Publication then advances the serialized publication ref under the predecessor accepted rules. Operational propagation begins only after that transition succeeds.

## Foreman

`Foreman` is execution-orchestration infrastructure, not automatic substantive authority.

The holder must be able to delegate work, schedule follow-ups, read canonical records, validate publication history, and preserve/recover concurrent package state. One holder may occupy Foreman bindings for several projects, but every action/state item remains project/plan-qualified; cross-project reach does not merge authority.

See `prompts/FOREMAN.md`.

## Work packages

Every substantive package must bind at least project/plan identity, exact current PlanRef, serving Role, typed target, bounded objective/scope, expected evidence, and return authority. Nested work must include the required parent bindings.

Temporary executors do not become Role holders merely by assignment.

Completion/evidence does not itself accept the Milestone. Acceptance and later roadmap projection remain separate.

## Publication notifications

Every published-change payload must bind to one validated publication transition, including at least:

```text
publication_id
publication_commit
new_plan_ref
prior_publication_id
prior_plan_ref
semantic_delta
active_work_impact
```

Before applying transition-specific actions, match the payload to validated publication history and durable last-applied state. Ignore duplicates; do not let stale/superseded messages reapply older actions. If notifications were skipped/out of order, reconcile valid transitions in order from last applied through CURRENT.

## Cross-repository nesting

Repositories keep independent Git histories. Parent/child authority comes from explicit contracts/delegations and exact accepted publication state, not forks/submodules/copied trees/repository ownership.

A child may bootstrap from accepted parent authority; it does not need an unrelated root founder.

## Domain-specific projects

Projects add their own safety, privacy, release, data-integrity, hardware, legal, and technical invariants. This template does not override them.
