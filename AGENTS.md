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

23. **Operational Foreman execution requires accepted `transition-action-v1` adoption.** `transition_action_contract: none` is no-autonomous-dispatch mode. Valid adoption/legacy-baseline reconciliation and verified required checks must precede dispatch/start/resume or any revision/attempt/rebind/supersession that creates execution obligations.

## Before any substantive planning or execution action

Resolve from accepted records:

- project/plan identity;
- adopted reference contract when cross-plan references are used; verified machine repository identity, repository-local PlanID and expected object kind/ID under `planning/REFERENCES.md`;
- bootstrap-configured publication ref;
- trusted publication journal kind/locator/trust basis;
- latest valid `publication_event_id`, `publication_commit`, `publication_id`, and current `plan_ref`;
- exact retained snapshot locator/evidence for that PlanRef;
- exact retained carrier evidence locator/evidence for the accepted publication carrier and any recovery suffix evidence required by its event;
- before using operational inventory state: fixed logical inventory locator/identity, serialization mechanism, coordination domain and history-retention contract with continuity from adoption under `planning/EXECUTION.md`; validate current writer/Foreman holder and claim separately. A same-version configuration move fails before publication; unavailable/contradictory state is not permission for a fallback store;
- before managed execution: current accepted `transition-action-v1` configuration and exact carrier path, valid adopting/legacy baseline with complete indexed/reconciled obligations and verified checks, and no publication-reconciliation failure blocking the affected action; an empty inventory under `none` does not authorize dispatch;
- when `transition-action-v1` applies: exact journal-bound carrier manifest, predecessor-valid approval, protected inventory-impact baseline and durable publication/dispatch fence evidence under `planning/PUBLICATION_TRANSITIONS.md` section 9;
- declared grammar;
- for Role authority: acting Role and its own current holder binding; for temporary execution: exact bounded authorization, authorizing Role/current binding, and executor identity under `planning/EXECUTION.md`;
- typed target and its own prerequisites/authority under `planning/EXECUTION.md`;
- authority source;
- exact authority revisions separately for external Role/source references; do not confuse a subject contract's PlanRef with an external accepting/delegating Role's PlanRef;
- when accepting a Milestone: exact `contract_plan_ref`, accepting Role, authority source, and evidence;
- when dispatch depends on DONE: current PlanRef must actually project DONE and index acceptance;
- when dispatch depends on an adopted Decision/DATA contract: current accepted PlanRef must index the exact operative result/resolution, and its contract/input/authority or objective usability checks must pass under `planning/NODE_CONTRACTS.md`;
- when nested: parent plan/ref/milestone/contract and grammar compatibility;
- before nested substantive dispatch/resumption: local readiness plus every applicable ancestor hard prerequisite and selected Decision branch, with current accepted state or explicit accepted opaque-boundary readiness evidence under `planning/NESTING.md`;
- when delegating: exact delegation capability.

Do not use unpublished default-branch governance, mutable ref freshness, local reflogs, or message arrival order as substitutes for trusted publication state. Follow `planning/PUBLICATION.md` and `planning/PUBLICATION_TRANSITIONS.md`.

If the trusted journal, required retained PlanRef snapshots, required retained carrier/suffix evidence, or accepted authority state is unavailable/invalid, ordinary dependent execution fails closed. Only bounded root/parent bootstrap or explicitly authorized recovery may proceed.

## Canonical files

Read together as applicable:

- `planning/PLAN.md` — roadmap.
- `planning/CONVENTIONS.md` — node/edge grammar.
- `planning/NODE_CONTRACTS.md` — explicitly adopted Decision results and DATA resolutions, current indices, replacement/withdrawal and migration.
- `planning/NESTING.md` — recursive delegation.
- `planning/REFERENCES.md` — cross-plan reference and parent revision roles.
- `planning/ROLES.md` — Role scopes/holders/capabilities.
- `planning/PUBLICATION.md` — bootstrap/publication model.
- `planning/PUBLICATION_TRANSITIONS.md` — normative journal, retention, recovery, and notification validation.
- `planning/EXECUTION.md` — typed targets, executor authorization, receipts, configured inventory, and succession.
- configured execution inventory (default `planning/EXECUTION_INVENTORY.md`) — package/attempt/route/result/check state; create from its template in an instantiated project.
- `planning/CURRENT.md` — carrier record on the publication ref.
- `planning/FOUNDING.md` — root founding record when applicable.
- `planning/PARENT.md` — parent relationship when nested.

The template source may ship templates rather than an instantiated operational plan.

## Creating or changing a plan

Use only the accepted grammar. State semantic delta, affected milestones/Roles, active-work impact, authority impact, Foreman dispatch requirement, and controlling evidence/decision.

A semantic candidate does not become current merely because it exists or merges. Approval binds the exact candidate; the candidate is durably retained; the publication ref moves under accepted governance; the exact carrier evidence is durably retained; and a trusted journal event commits that exact transition before operational propagation begins.

For adopted `transition-action-v1`, prepare the complete immutable transition-action manifest before approval; predecessor-valid approval binds its exact blob/record ID as well as the candidate. Put it in the successor carrier and bind it in the trusted journal, using existing carrier retention. Every governed publication has explicit impact/no-impact evidence. Conditionally acquire its preallocated durable fence against the exact analyzed baseline in the same mechanism as dispatch claims; changed baseline requires rebuild/reapproval. Hold through valid journal commit and durably release afterward. Follow the canonical failure/recovery, no-impact/bootstrap and legacy rules; neither a reread nor timeout bypasses the fence, and a candidate cannot authorize its own manifest/fence.

## Foreman

`Foreman` is execution-orchestration infrastructure, not automatic substantive authority. Under `transition_action_contract: none`, it may maintain inventory/read-only coordination under valid authority but cannot dispatch/start/resume or create execution obligations. Material publication affecting active/outstanding legacy obligations requires prior-authorized reconciliation/adoption or durable stop under valid legacy rules; do not invent missing action payloads. See `planning/PUBLICATION.md` for the sole supported operational reconstruction contract and eligibility boundary.

The holder must be able to delegate work, schedule follow-ups, read canonical records, validate trusted publication history/retained PlanRefs/retained carrier evidence, and preserve/recover concurrent package state. One holder may occupy Foreman bindings for several projects, but every action/state item remains project/plan-qualified; cross-project reach does not merge authority.

See `prompts/FOREMAN.md`.

## Work packages

Every substantive package must bind project/plan identity, immutable accepted package authorization/target-binding `plan_ref`, immutable package revision, serving Role, `target_type`/`target_id`/`target_record`, bounded objective/actions, explicit executor authorization, expected evidence, and return authority/route. Before first dispatch, every resume or other obligation-creating action, separately record the exact current accepted PlanRef/event and full current-sensitive validation in the attempt/inventory under `planning/EXECUTION.md`. An unrelated later PlanRef does not rewrite a still-valid package baseline; it never excuses current checks. Nested work includes required parent bindings. Use `planning/EXECUTION.md` and `templates/WORK_PACKAGE.md`.

Temporary executors validate their own bounded authorization and its authorizer's current accepted authority, not a fictional claim to hold the serving Role. Assignment grants no acceptance, reserved Decision, Role-binding, or re-delegation authority. Rebinding/revocation and bounded execution checkpoints follow `planning/EXECUTION.md`. Completion/evidence does not itself accept a Milestone or decide a Decision.

Before dispatch/start/resume or any obligation-creating/broadening coordination mutation, validate operational eligibility under `planning/EXECUTION.md`, then check current publication fences through the same serialized inventory mechanism and block within held scope. Durably claim/index the exact attempt and verify required follow-ups. On succession or uncertain delivery/execution, reconcile the existing attempt, routes, results, receipts, and actual scheduler state before retrying/replacing it. Missing state never permits speculative redispatch.

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

Under `transition-action-v1`, reconstruct lost-wake actions from that event's exact retained manifest, not PR history or notification prose. Index/reconcile every missing request/recipient receipt/check before advancing `last_reconciled_publication_event`; a validated empty manifest creates no receipts, while an affected `continue` is explicit. Apply the separate legacy-baseline rules rather than fabricating historical manifests.

Material changes require durable per-attempt receipts: recorded, sent/wake attempted, delivered, acknowledged, applied, and closed are separate facts. A sent or acknowledged pause is **not confirmed stopped** without application/enforcement evidence. Foreman maintains a verified publication reconciliation check and receipt timeout/recovery checks; affected executors follow bounded revalidation/stop rules in `planning/EXECUTION.md`.

## Cross-repository nesting

Repositories keep independent Git histories. Parent/child authority comes from explicit contracts/delegations and exact accepted publication state, not forks/submodules/copied trees/repository ownership.

A child may bootstrap from accepted parent authority; it does not need an unrelated root founder.

The parent contract's prior authority baseline, the accepted relationship revision pinned by the child, and current parent authority are distinct. Resolve them under `planning/REFERENCES.md`; do not manufacture self-containing commit references or treat a historical pin as permanent authority.

## Domain-specific projects

Projects add their own safety, privacy, release, data-integrity, hardware, legal, and technical invariants. This template does not override them.
