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
15. **Plan-change notifications are wake mechanisms, not authority.** Apply transition-specific actions only after matching them to accepted publication state.
16. **Exact accepted Git commits are PlanRefs.** Mutable branches are locators only.
17. **Current planning state comes from a trusted publication journal.** The latest valid committed journal event, plus its retained exact PlanRef and retained carrier evidence, establishes the accepted high-water mark. A mutable publication ref or Git ancestry alone is insufficient to prove past ref movements.
18. **Published PlanRefs and accepted carrier evidence must remain durably fetchable.** Every accepted exact PlanRef and every accepted publication carrier has retained evidence independent of ordinary branch cleanup, squash, rebase, live-ref reachability, and garbage collection. Recovery also retains the invalid suffix evidence required for cold validation.
19. **The predecessor accepted rules validate the next publication transition.** Candidate governance cannot validate the transition that makes itself current.
20. **Normal publication is serialized and externally evidenced.** A normal carrier advances conditionally/non-force from the exact accepted incumbent, and a trusted journal event records the successful old->new ref update.
21. **Invalid publication suffixes are preserved, not adopted.** Recovery may fast-forward over an invalid/uncommitted actual tip while naming the last valid accepted carrier separately; invalid suffix content does not become accepted governance.
22. **Root bootstrap is one bounded external exception.** A root project may use an explicitly designated Founding Authority only to establish its first accepted state and initial publication/journal/PlanRef-retention/carrier-retention trust contract. The exception expires after first valid journaled publication.

## Before any substantive planning or execution action

Resolve from accepted records:

- project/plan identity;
- bootstrap-configured publication ref;
- trusted publication journal kind/locator/trust basis;
- latest valid `publication_event_id`, `publication_commit`, `publication_id`, and current `plan_ref`;
- exact retained snapshot locator/evidence for that PlanRef;
- exact retained carrier evidence locator/evidence for the accepted publication carrier and any recovery suffix evidence required by its event;
- declared grammar;
- acting Role and current holder binding;
- target Milestone/Decision/scope;
- authority source;
- when accepting a Milestone: exact `contract_plan_ref`, accepting Role, authority source, and evidence;
- when dispatch depends on DONE: current PlanRef must actually project DONE and index acceptance;
- when dispatch depends on an adopted Decision/DATA contract: current accepted PlanRef must index the exact operative result/resolution, and its contract/input/authority or objective usability checks must pass under `planning/NODE_CONTRACTS.md`;
- when nested: parent plan/ref/milestone/contract and grammar compatibility;
- when delegating: exact delegation capability.

Do not use unpublished default-branch governance, mutable ref freshness, local reflogs, or message arrival order as substitutes for trusted publication state. Follow `planning/PUBLICATION.md` and `planning/PUBLICATION_TRANSITIONS.md`.

If the trusted journal, required retained PlanRef snapshots, required retained carrier/suffix evidence, or accepted authority state is unavailable/invalid, ordinary dependent execution fails closed. Only bounded root/parent bootstrap or explicitly authorized recovery may proceed.

## Canonical files

Read together as applicable:

- `planning/PLAN.md` — roadmap.
- `planning/CONVENTIONS.md` — node/edge grammar.
- `planning/NODE_CONTRACTS.md` — explicitly adopted Decision results and DATA resolutions, current indices, replacement/withdrawal and migration.
- `planning/NESTING.md` — recursive delegation.
- `planning/ROLES.md` — Role scopes/holders/capabilities.
- `planning/PUBLICATION.md` — bootstrap/publication model.
- `planning/PUBLICATION_TRANSITIONS.md` — normative journal, retention, recovery, and notification validation.
- `planning/CURRENT.md` — carrier record on the publication ref.
- `planning/FOUNDING.md` — root founding record when applicable.
- `planning/PARENT.md` — parent relationship when nested.

The template source may ship templates rather than an instantiated operational plan.

## Creating or changing a plan

Use only the accepted grammar. State semantic delta, affected milestones/Roles, active-work impact, authority impact, Foreman dispatch requirement, and controlling evidence/decision.

A semantic candidate does not become current merely because it exists or merges. Approval binds the exact candidate; the candidate is durably retained; the publication ref moves under accepted governance; the exact carrier evidence is durably retained; and a trusted journal event commits that exact transition before operational propagation begins.

## Foreman

`Foreman` is execution-orchestration infrastructure, not automatic substantive authority.

The holder must be able to delegate work, schedule follow-ups, read canonical records, validate trusted publication history/retained PlanRefs/retained carrier evidence, and preserve/recover concurrent package state. One holder may occupy Foreman bindings for several projects, but every action/state item remains project/plan-qualified; cross-project reach does not merge authority.

See `prompts/FOREMAN.md`.

## Work packages

Every substantive package must bind at least project/plan identity, exact current PlanRef, serving Role, typed target, bounded objective/scope, expected evidence, and return authority. Nested work includes required parent bindings.

Temporary executors do not become Role holders merely by assignment. Completion/evidence does not itself accept a Milestone.

## Publication notifications

Every published-change payload binds to one trusted committed publication event, including at least:

```text
publication_event_id
publication_id
publication_commit
new_plan_ref
prior_publication_id
prior_plan_ref
semantic_delta
active_work_impact
```

Before transition-specific actions, match the payload to validated journal state and retained carrier evidence plus durable last-applied state. Ignore duplicates; do not let stale/superseded messages reapply older actions. Reconcile skipped/out-of-order events in trusted journal order.

## Cross-repository nesting

Repositories keep independent Git histories. Parent/child authority comes from explicit contracts/delegations and exact accepted publication state, not forks/submodules/copied trees/repository ownership.

A child may bootstrap from accepted parent authority; it does not need an unrelated root founder.

## Domain-specific projects

Projects add their own safety, privacy, release, data-integrity, hardware, legal, and technical invariants. This template does not override them.
