# Work execution and recovery

This is the shared Foreman–executor contract for typed packages, temporary executor authorization, material-change receipts, and durable recovery. It supplements the accepted roadmap grammar; it does not change node classes, prerequisite satisfaction, Role delegation, or the publication protocol.

This template source is not an operational execution inventory. An instantiated project adopts/configures this contract through its normal accepted publication process before using it.

## Operational eligibility

Before any Foreman-managed substantive dispatch, start or resume, including a new package revision/attempt, executor/recipient rebind or supersession that creates execution obligations, validate and retain evidence of all four checks:

1. Resolve current accepted `plan-publication-v1` state from the trusted journal and retained PlanRef/carrier evidence.
2. The current accepted publication configuration explicitly adopts `transition-action-v1`; its exact path is fixed by the validated adopting event and preserved through every later v1 event under `PUBLICATION_TRANSITIONS.md` section 9. That path must equal the journal binding and resolve to its valid manifest in the exact carrier. A candidate declaration, changed v1 path or manifest at an unconfigured path is insufficient.
3. The required adopting event and legacy baseline are valid; their complete carried obligations are durably indexed/reconciled with required checks verified.
4. Publication reconciliation has no unresolved failure blocking the affected execution. Reconcile the relevant journal history and outstanding actions before treating the target as eligible; absent reconciliation evidence is not permission.

These checks supplement authority, target prerequisites, executor authorization and the serialized fence guards below. Validate the fixed inventory contract and its continuity from operational adoption under **Configuration and durable records** before relying on inventory/reconciliation state; an unavailable or contradictory configured mechanism fails closed. These checks do not themselves authorize work. Recheck current eligibility at the action; an old package validation cannot preserve permission after current configuration or reconciliation state changes.

`transition_action_contract: none` is no-autonomous-dispatch mode. Inventory maintenance/read-only coordination may continue under valid authority, but neither an empty inventory nor an accepted Foreman/worker binding permits creating or starting an executor attempt. Commissioned read-only research is still an execution obligation; it is not merely observing the inventory. For legacy active/outstanding work under `none`, block new dispatch/resume and material publication that would alter those obligations pending the prior-authorized reconciliation/adoption or durable legacy stop described in `PUBLICATION.md`. Never guess a missing pause payload from notification text or current worker state.

Only `transition-action-v1` currently supplies the supported operational reconstruction contract. An initial alternate inventory representation or provider-specific fence implementation must preserve that adopted contract and the fixed inventory rules below; it is not permission for a later same-version inventory/mechanism move. External template-source maintenance continues to use its actual external authorization, not invented operational bindings.

## Configuration and durable records

The accepted project configuration in this file must identify:

```text
execution_inventory_locator: planning/EXECUTION_INVENTORY.md
execution_inventory_identity: <stable logical inventory identity within this PlanID>
inventory_serialization_contract: <exact logical conditional-update/dispatch-claim mechanism>
inventory_coordination_domain: <exact shared coordination domain/scope>
inventory_history_retention_contract: <required durable history and cold-discovery semantics>
inventory_write_policy: <authorized writer Roles/rules; validate current holder and claim at use>
publication_reconciliation_interval: <finite maximum interval>
receipt_ack_timeout: <finite interval>
receipt_apply_timeout: <finite interval after acknowledgement>
recovery_escalation_route: <Role and reachable fallback route>
```

Replace placeholders before operational dispatch. First operational adoption may select the initial exact inventory locator/identity and mechanism, including an alternative such as an issue index, under predecessor-valid/root/parent authority and the complete legacy/adoption baseline rules. After operational adoption these logical bindings are fixed for this PlanID/execution-contract lifetime. A branch, chat memory, worker's unindexed report or similarly populated store cannot replace the configured inventory.

The inventory is authoritative for **coordination state**, not for planning authority. Foreman may update runtime records under accepted coordination permissions without publishing a new PlanRef for every check. Preserve exact package revisions, prior attempts, requests/receipts, results, and state-change evidence in recoverable history. Serialize inventory changes and dispatch claims through the configured mechanism (for example, conditional versioned updates that reject a stale inventory revision); a pre-write read alone is insufficient. A claim binds its ID, inventory revision, current holder/binding and prior claim disposition. Check the current claim before each dispatch or other coordination mutation; stale holders/claims must fail. If a claim/update has an unknown outcome, reconcile it before retrying.

Use `templates/EXECUTION_INVENTORY.md`, `templates/WORK_PACKAGE.md`, and `templates/EXECUTION_RECEIPT.md`. The initially adopted representation must preserve all required fields and transitions. Discover the full outstanding set from that fixed configured inventory, including prepared/dispatched attempts, material receipts, and schedules; do not require knowledge of old chat IDs to discover it.

Every record is project/plan-qualified using the existing plan identity rules. Local package IDs, Role names, and schedule IDs alone are not globally unique. This requirement does not create cross-project authority.

### Fixed inventory contract and permitted runtime changes

Once operational execution is adopted/enabled, the logical `execution_inventory_locator`/identity, conditional-serialization mechanism, coordination domain/scope and required history-retention semantics are fixed for this PlanID and execution-contract lifetime. History must retain cold-discoverable packages/revisions/attempts, claims, requests/receipts, results, scheduler records, reconciliation/application markers and active/uncertain fences. Before publishing a later candidate under this same contract version, validate that it preserves all four bindings. A change to any of them is unsupported and MUST fail before publication/ref movement, even if rows are copied or the new store appears equivalent. A future move needs a separately specified/versioned migration contract; none is defined here. If the configured mechanism is unavailable or contradictory, fail closed; do not silently start a fallback inventory.

These fixed bindings do not freeze ordinary rows/revisions or a human/process holder. Within the same mechanism/domain, package/receipt/result/check/fence lifecycles, Foreman/writer succession and serialized claim handoff remain governed by their existing rules. `inventory_write_policy` names writer authority/rules separately from the fixed mechanism; validate the writer's current accepted authority and claim at use. Authorized credential/session/route replacement and evidenced scheduler-ID replacement may proceed with retained old/new state and evidence, without losing history or moving the coordination domain. Provider implementation upgrades are permitted only with evidence that they preserve the same accepted logical conditional-serialization/history contract; a new store/domain is not such an upgrade.

An individual publication fence still selects its affected scope inside this fixed coordination domain under `PUBLICATION_TRANSITIONS.md`; fence creation/transition/release is runtime state, not a domain migration. Holder/claim succession does not clear an active/uncertain fence or close an outstanding receipt.

### Publication/dispatch fences

For adopted `transition-action-v1`, this **same serialized inventory/dispatch mechanism** durably records publication fences under `PUBLICATION_TRANSITIONS.md` section 9. A fence names its exact domain/scope, analyzed baseline/obligation set, stable preallocated ID, candidate/manifest/transition identities and acquisition/continuity/release evidence. Discover all active/uncertain fences from the inventory; they are coordination-safety records, not authority or a second currentness journal.

Every obligation-creating/broadening dispatch, start, resume, new package revision/attempt, executor/recipient rebind or other coordination mutation must check the current fence in the same serialized operation and block/fail within its scope while held. This includes work created by a scheduler/wake and dispatch claims prepared before acquisition. A stale pre-read is insufficient; a dispatch-capable path outside the mechanism invalidates the claimed coverage. The fence's domain covers potential affected attempts, not only those already listed in a manifest. Known unrelated work can proceed only outside that exact domain.

Pure observations or obligation-reducing evidence may be recorded while fenced only when they cannot create/broaden execution obligations; preserve the classified change. Acknowledgement, a return or cessation evidence is not a new execution grant. Existing in-flight effects remain subject to their bounded execution/stop contract and transition receipts; acquiring this coordination fence does not prove cessation or replace external effect fencing.

Acquire conditionally against the exact approved impact baseline after approval and before ref movement; changed baseline requires rebuild/reapproval. Hold through valid journal commit, then durably release and validate successor current state before later dispatch. Retention/journal failure after ref movement leaves both an uncommitted suffix and a durable fence until explicit recovery or verified abort/suffix reconciliation permits release. Journal success with failed release keeps execution conservatively blocked. Follow section 9 for all abort/recovery/bootstrap/legacy paths; neither timeout/lease expiry nor succession clears a fence.

## Typed targets

Every package binds `target_type` and `target_id` at its immutable `plan_ref`: the exact accepted package authorization/target-definition baseline, not a field to overwrite with later current state.

| `target_type` | `target_id` resolves to | Dispatch and return boundary |
|---|---|---|
| `milestone` | An existing Milestone | Its own prerequisites and contract govern execution. Return evidence to the named substantive authority; delivery does not accept it. |
| `decision` | An existing Decision | Its own prerequisites and authorized research/review scope govern preparation. `return_to` is its unique deciding Role; evidence is not that Role's judgment. |
| `data` | An existing DATA node | Its own dependency/evidence contract and accepted producing scope govern work. Producing an artifact does not establish satisfaction beyond the accepted node rules. |
| `plan-maintenance` | A stable bounded maintenance scope in an accepted record named by `target_record` | The accepted scope names its authority, inputs, and limits. This is a work classification, not a new roadmap node or exemption from governance. |

Record `target_record` for every type so the exact definition at the package `plan_ref` can be retrieved and interpreted. Current accepted state determines whether relying on that frozen definition remains permitted. No target type supplies authority by itself. Do not assign Roles to Gates, invent Milestones for activities, or infer Decision/DATA activation rules from this table. Use the current accepted `CONVENTIONS.md` for those rules; unresolved semantics block only the dependent action.

A standalone Decision research package does not require a downstream Milestone. It cannot execute a downstream outcome whose prerequisites remain closed. In a child plan, retain the actual parent Milestone/contract binding required by `NESTING.md`; that parent boundary is distinct from the local typed target.

`plan-maintenance` here concerns an instantiated plan with accepted scope. External maintenance of the template source uses its actual external authorization and source revision; do not fabricate an operational PlanID, target node, or accepted PlanRef for that work.

## Authority holder and temporary executor

Two checks are distinct:

1. A **Role holder** making a substantive decision or exercising Role authority validates its own current accepted Role/holder binding and authority source.
2. A **temporary executor** validates a durable bounded authorization for its exact identity/context and package revision. It does not claim to be the serving or authorizing Role's holder.

The authorization must identify the authorizing Role, issuing holder, exact accepted binding reference, independent authority source, executor identity/context, permitted actions/tools/resources/scope, validity limits, revocation conditions, and reserved decisions. Its source must already permit that Role to commission those actions inside its existing scope. Naming a Role, assigning a Milestone, or possessing a tool is insufficient. An executor must be able to fetch these records and validate current publication/authority state, or stop the affected work.

Foreman records/routes authorization issued by a qualified authorizing holder. Foreman cannot manufacture it from its coordination Role. A standing authorization may cover a precisely bounded class of packages only when an independently accepted source explicitly grants that arrangement; record that source and how this exact package/executor meets its limits.

The permitted action set only narrows the authorizing Role's existing permissions. Temporary execution is not Role-to-Role delegation and does not grant any capability from `NESTING.md`. This authorization never permits the executor to bind Roles, accept Milestones, make reserved Decisions, re-delegate substantive authority, or commission another executor. If the same person separately holds such authority, they must switch to and validate that distinct Role/authorization path, with a separate record. The package cannot supply that authority.

Record explicit validity bounds: start condition, expiry or completion condition, permitted exact input revisions, maximum uninterrupted execution segment, checkpoint policy, and stop/revocation conditions. Missing bounds are not unlimited permission. Rebinding/vacating the authorizing Role, changing the executor identity, or materially changing its authority/scope suspends the affected authorization pending explicit revalidation/reissue by the current authorized holder. Foreman succession alone does not rebind the substantive Role or silently replace the executor.

## Package baseline and current validation

The immutable package `plan_ref` identifies the exact accepted state under which this package revision was issued and its target, inputs, scope and authorization evidence were bound. Before first dispatch, every resume and any other obligation-creating action, separately resolve current accepted state and durably record `current_checked_plan_ref_and_publication_event` in the attempt/inventory. Reconcile accepted publication history through that exact event and retain `current_validation_evidence_and_conclusion` for all current-sensitive checks:

- operational eligibility, explicit `transition-action-v1` adoption/baseline and outstanding publication/material-action reconciliation;
- current Role/holder bindings, authorizer authority and executor-grant validity;
- continued target applicability and its prerequisites, including currently operative Decision/DATA evidence, dependency-satisfiability conformance under `SATISFIABILITY.md`, and the full ancestor-readiness check when nested;
- exact input revisions and their continued permitted use;
- current publication/dispatch fences through the existing serialized guard;
- revocation, scope or semantic changes affecting the package.

A current-check field or a matching target file alone proves none of these predicates. The package baseline and current validation must never be collapsed. An unrelated new PlanRef does not force restart or reissue: a package prepared or paused at P1 may first dispatch/resume while P2 is current only after those checks prove its original package/authorization remains valid and any prior stop is validly disposed. Preserve P1, the original revision and evidence. Material changes to target meaning, permitted scope/inputs, required authority, executor grant, reserved decisions or another package-defining contract follow the existing suspend/revalidate/new-authorized-revision path; do not edit an issued grant in place or treat its historical validity as current permission.

## Dispatch and attempts

Separate the stable package ID, immutable `package_revision`, and per-executor `attempt_id`. The inventory contains one current dispatch claim for each package, binding its exact revision and attempt. A new revision or supersession label cannot bypass reconciliation of its predecessor's execution. Multiple intentional parallel assignments require separate bounded packages; retries are not extra authority.

Before sending work:

1. Perform and durably record **Package baseline and current validation** above, including all operational eligibility checks, current publication/retention/authority, typed target prerequisites, authorization, executor route, and exact input revisions. Repeat before every resume or other obligation-creating action; do not substitute the immutable package `plan_ref` for current validation.
2. Through the same serialized mechanism, check current publication fences and persist a durable claim containing the package/revision, attempt ID, executor/return routes, current authorization, state `dispatch-pending`, and recovery obligation. A fence blocks affected obligation-creating/broadening claims. Create and verify a real scheduled check whenever any dispatch acknowledgement, return, or future condition will be asynchronous; persist its ID, owner, trigger, and evidence before dispatch.
3. Send the exact package/revision and attempt ID only under the current serialized fence/dispatch guard; an old claim cannot bypass an intervening fence. Record each transport attempt and its observed outcome. An ambiguous send leaves `dispatch-pending`/unknown execution, not permission to create another attempt.
4. The executor acknowledges the exact assignment and starts/resumes only after validation, including the same serialized fence guard for obligation-creating/broadening actions. It deduplicates repeat delivery of that attempt, returning current state or existing results instead of starting again. Foreman records `running` only with executor/start evidence.

If the transport cannot deduplicate an ambiguous dispatch, use a read-only query/reconciliation route. Do not resend an executable assignment until the old attempt is proved not started, terminal, or effectively fenced from further effects. A newly created executor context is a new attempt requiring a new authorization binding.

| Package coordination state | Meaning |
|---|---|
| `draft` / `authorized` | Exists / exact authorization is recorded; neither proves dispatch. |
| `dispatch-pending` | Claim exists; delivery/start is being reconciled. |
| `running` | The exact executor acknowledged and reported starting. |
| `pause-requested` | A material stop is outstanding; execution is **not confirmed stopped**. |
| `paused` | Applied receipt or verified enforcement proves the stated scope stopped, with in-flight work disposition. |
| `blocked` / `unknown` | A known blocker / insufficient evidence of execution state. Neither means stopped. |
| `returned` | Durable result was indexed. This is evidence, not substantive acceptance. |
| `cancelled` / `superseded` | No further execution is permitted and cessation is evidenced; retain predecessor/result links. |
| `closed` | Return routed, coordination obligations settled, and schedules reconciled. This does not accept a planning outcome. |

Keep actual execution observation separate from package state. A pause request over a `returned` attempt still needs reconciliation of any remaining tools/jobs; a package label alone cannot stop them.

## Material requests and receipts

Material pause, revocation, scope reduction, redirection, or supersession must have a durable request before a wake is attempted. Record one receipt per **request + affected recipient identity/context + exact package revision/attempt**. Within the recorded project/plan context, the key is `request_id`, `recipient_identity_context`, `work_package_id`, `package_revision`, and `attempt_id`. `templates/EXECUTION_RECEIPT.md` supplies the minimum fields.

Direct, fallback, retry, webhook, prompt, or other routes to that same recipient/attempt are transport attempts inside that one receipt; a route is not part of its key. Retain each route's historical observations, including failed/rejected/unknown attempts, without overwriting them when another route succeeds. A different independently obligated recipient/context or package revision/attempt has a different receipt. A nested coordinator that must itself acknowledge/apply an action is a separate recipient; a mere transit hop is not automatically another obligation.

For a published change, bind the full publication payload required by `PUBLICATION_TRANSITIONS.md`, the exact package revision/attempt, requested action, recipient, supersession relationship, and deadlines. Validate journal/retained-carrier identity before applying a transition. For a stop issued under an existing authorization's revocation terms, cite that exact authorization, current issuing Role/binding, and durable stop record. This second path can restrict execution within its existing authority; it cannot publish changed plan governance or grant resumed/new scope.

Preserve these separate facts; evidence for one does not imply the next:

| Fact | Required meaning |
|---|---|
| `recorded` | Durable request exists and is inventoried. |
| `sent` / `wake attempted` | A transport attempt was made; record success, rejection, or unknown outcome. |
| `delivered` | Transport evidence confirms receipt at the specified destination. If unavailable, leave unknown; an exact recipient acknowledgement can also establish receipt. |
| `acknowledged` | The recipient durably identifies the exact request, package/revision/attempt and understands the required action, including any inability to apply it. |
| `applied` | Durable evidence identifies what actually changed/stopped, when, the last action/revision, in-flight jobs/side effects, and any remaining limitations. |
| `closed` | Foreman reconciled the recipient's requested obligation, application evidence and follow-up disposition, or a validated later request explicitly superseded it. Closure does not require every transport route to succeed. |

Acknowledgement of a pause is not confirmation of cessation. `paused`, cancelled execution, or effective revocation may be reported only for the exact scope supported by applied evidence or verified enforcement. If a subprocess continues, state that explicitly and keep the stop outstanding. No wording such as `sent`, `delivered`, `done`, or `closed` may silently promote weaker evidence to proof of stopped execution.

A failed route remains retained transport evidence, not a second independently outstanding receipt after another route satisfies the same recipient's obligation. Acknowledgement through a fallback still leaves application outstanding when required. A different receipt does not automatically close an earlier obligation; closure requires its reconciliation or explicit valid supersession.

Durable material records are transport-independent. Direct prompts, webhooks, explicit child messages, or scheduled polling may wake a receiver. A worker's bare completion event is not a guaranteed notification. A rejected send, including an archived/unreachable target, is not delivery and does not authorize unarchiving or changing its lifecycle.

## Lost requests and continued execution

Operational Foreman execution requires both recovery loops below, and therefore current accepted `transition-action-v1` adoption plus valid baseline reconciliation before dispatch. A `none` configuration can perform read-only discovery, but cannot use discovery as permission to dispatch or invent absent historical actions.

- **Publication to Foreman:** maintain a verified scheduled reconciliation at the configured maximum interval. Reconstruct every newly accepted transition's obligations from its exact retained `transition-action-v1` manifest using the procedure below, even when no notification arrived. The current worker set or notification prose cannot supply missing approved actions.
- **Foreman to executor:** before relying on a material request, schedule and verify its acknowledgement/application checks, indexed to that receipt. Foreman owns timeout handling: retry an authorized supported wake route, query the executor/effects, use a known fallback route, and escalate to the configured authority if still unresolved. Acknowledgement without application still needs its application deadline and recovery check. Failed scheduling is `ACTION NEEDED`; an unscheduled future intention is not recovery.

If a missing or pre-adoption reconciliation marker precedes the approved adoption baseline, first validate the legacy history and adopting event under `PUBLICATION_TRANSITIONS.md` section 9. Use that exact baseline to reconstruct the explicitly carried legacy obligations together with the adoption actions; do not demand manifests for the covered pre-adoption events. The procedure below starts with the adopting event, and its marker may advance only after the baseline's complete obligations are indexed/reconciled. A claimed legacy high-water without valid reconciliation evidence cannot initialize the marker.

For each applicable committed event after `last_reconciled_publication_event`, in trusted journal order:

1. Validate the event, retained PlanRef/carrier and predecessor governance under `PUBLICATION_TRANSITIONS.md`, including section 9's first-path adoption/fixed-path equality rule. Fetch the configured manifest from that exact carrier and verify the journal-bound contract/path/blob/record ID; do not use the manifest at a newer carrier's same path or infer path migration from a duplicate file.
2. Validate the exact predecessor/candidate/event/publication identities, action authority, approval binding and retained inventory-baseline/completeness evidence, including matching fence ID/scope, conditional acquisition and held-through-valid-commit proof (or permitted bootstrap basis). Read each explicit affected attempt and recipient obligation, including `continue`. A no-impact conclusion is usable only with a valid explicit empty manifest and its protected basis. Missing/mismatched records, fence proof or unresolved legacy coverage block affected execution and marker advancement.
3. Under the current serialized coordination claim, reconcile each stable manifest request ID and full receipt key against the inventory. Create/index every missing request and recipient receipt with the exact action payload, target/scope, authorization/source, routes, anchored deadlines and predecessor/supersession relation. Preserve prior delivery/application and failed route history. Resolve journal/carrier fields from this event; never synthesize a new request identity or assume an absent attempt is stopped merely because current inventory no longer lists it.
4. Reconcile every specified logical recovery check and record its actual verified scheduler ID/owner/trigger or unresolved recovery blocker. Do not duplicate possibly live checks; use the existing scheduler procedure. Already overdue obligations trigger immediate authorized recovery with their original deadlines retained. Index requests/receipts before any wake. If verification fails, leave the event pending, fail closed for affected execution and escalate; a placeholder task ID is not a verified check.
5. Only after **all** event obligations are durably indexed/reconciled and required checks verified may the serialized `last_reconciled_publication_event` advance. A crash partway through resumes missing obligations under the same IDs, without duplicate dispatch. Valid empty impact permits advancement without receipts. Indexed is not applied: per-attempt application/closure remains a separate marker and evidence requirement.

The record schema and publication/adoption order are in `templates/TRANSITION_ACTION.md` and `PUBLICATION_TRANSITIONS.md` section 9. Explicit adoption and reconciled baseline are mandatory for operational eligibility, including the first dispatch. Pre-adoption events retain their historical rules; reconcile their execution obligations during adoption rather than inventing old manifests or inferring actions from PR history. Unknown legacy obligations cannot be skipped. No second action/currentness journal is introduced.

While a material authority/scope restriction remains unapplied, Foreman blocks new dependent dispatch, replacement execution, resumption, and final readiness/acceptance handoffs. Preserve unaffected work. Report the affected attempt as **not confirmed stopped**, including the exposure interval and last verified action. A timeout or unavailable worker is not evidence that it stopped.

Each executor revalidates current operational eligibility, publication/authority and outstanding requests at the package's bounded execution checkpoints, as well as before new/resumed substantive work and final handoff. If it cannot validate, it starts no further segment and follows its preauthorized safe-stop procedure. A non-interruptible action must have an explicit bounded duration/effect and stop procedure before it starts. This bounds cooperative operation; messaging alone cannot instantly halt already-running effects or an unreachable worker.

Projects needing stronger guarantees may require fail-closed leases/heartbeats and external fencing. Such a policy must define expiry, renewal authority, enforcement point, clock/failure assumptions, and proof of effect cessation. An unenforced lease timestamp is not a fence. If the configured stop bound cannot be met, do not dispatch that work under a best-effort assumption.

Reconcile publication-driven requests in trusted journal order. Keep `last_reconciled_publication_event` separate from `last_applied_publication_event` per attempt. Duplicate applied requests are no-ops; stale requests cannot undo a later valid application. A later `continue` cannot erase an unresolved earlier stop: validate the intervening history and explicit disposition of that stop, then obtain valid reauthorization before resumption. Preserve old requests and link any superseding applied receipt.

## Scheduler inventory and succession

Inventory every publication watch, package check, receipt retry/application check, and cleanup obligation. Each needs a stable logical check ID, package/receipt relation or explicit plan-wide purpose, scheduler/task ID, concrete execution owner/context, target route, exact trigger/cadence/time zone, action/prompt locator, last verified state/time/evidence, next due time, and replacement/cleanup disposition. Record context reachability separately from task liveness.

On startup, succession, or capability loss:

1. Validate current accepted publication state; for operationally adopted execution, validate the inventory identity/mechanism/domain/history continuity from adoption, then locate that same configured inventory. Unavailable/contradictory state blocks dependent execution; no fallback store or ad hoc copy substitutes. Check operational eligibility before any dispatch/obligation-creating mutation; `none` permits only bounded inventory/read-only coordination and valid legacy reconciliation. Acquire the serialized coordination/dispatch claim under current Foreman binding before making mutations; a prior holder cannot continue using an obsolete claim. Discover active/uncertain publication fences, their exact transitions and acquisition/release history; apply section 9 recovery before affected dispatch. A replaced Foreman or expired lease does not clear them.
2. Reconstruct each nonterminal package revision/attempt, executor route, authorization, last applied event, material receipt, exact result, and check. Preserve historical records. Mark unsupported old liveness claims `unknown`.
3. Query actual executor and scheduler state through available read-only routes. Reconcile results and in-flight effects before any dispatch retry or replacement. A durable result may settle a returned package even when its old executor is unreachable; absence of a result cannot prove non-execution.
4. Classify each outstanding check as `verified-live`, `recreated`, `completed`, or `lost/cancelled`, with evidence. If verification is unavailable, retain `unknown` as an unresolved blocker; do not force it into a proven class. Recreate a missing check only after resolving an old possibly live check or ensuring duplicate wakeups are harmless and idempotent. Index the replacement ID/owner and disposition of the old one. Follow-up checks must reconcile before dispatching, so a duplicated wake never authorizes duplicated execution.
5. Reconcile journal gaps and outstanding receipts, restore verified future checks, and revalidate active authorizations. Resume coordination of the existing attempt when valid; do not issue a fresh executor merely because the Foreman changed.
6. If replacement execution is necessary, prove the prior attempt terminal/not started or effectively fenced; record that evidence, its results/effects, a linked new attempt and current authorization. Otherwise preserve `unknown`/`pause-requested`, schedule recovery if possible, and escalate. Never trade missing state for speculative redispatch.

Schedule lifecycle depends on the execution substrate. Do not infer that archive equals deletion, that an ancestor's retirement removes descendant work, or that unarchiving restores schedules. Verify the actual context/resource owner and each task's state. A task ID or a UI card without an existence/status result is not liveness proof.

Externalize results, inventory, and recovery routes before a planned holder teardown. Cleanup disposition is an independently evidenced fact, not a side effect inferred from retirement. Generic worker cleanup permission does not authorize destroying a multi-context project/container; exact destructive scope needs its own authority. No universal lifecycle behavior or Foreman topology is implied.

## Execution-context capability profiles

Keep a small durable capability profile for each actual execution environment/context used for coordination, including relevant containing resources, in the existing configured inventory using `templates/EXECUTION_INVENTORY.md`. It describes runtime capabilities, not Role authority, plan identity, publication currentness or a different inventory mechanism. Profile updates use the existing serialized writer/claim and history rules. A new holder/context may need a new or revalidated profile; this does not move the fixed inventory or change the succession procedure above.

Bind a profile ID/revision to the exact runtime resource identity and locator, provider/environment kind, relevant tool/route/configuration or target mode, and container relationship. Use actual substrate resource IDs within the existing project/plan context, not display names alone; this creates no new qualified-reference scheme. Record read/send/recovery route limitations and link the corresponding executor attempts and scheduler records. Record the schedule's actual owning resource and its relation to the context/container, separately from the notification target or logical Role holder. If identity/ownership cannot be established, retain `unknown` and block reliance that requires it.

The minimum facts are:

```text
context_kind
create_supported
creation_constraints_or_target_modes
archive_supported
unarchive_supported
permanent_delete_supported
child_creation_supported
scheduled_task_supported
schedule_owner
archive_effect_on_own_schedules
archive_effect_on_descendants
unarchive_effect_on_schedules
archived_target_reachability_or_delivery_behavior
project_or_container_delete_supported
deletion_scope
capability_evidence_and_last_verified
```

Every support field uses `supported | unsupported | unknown`. `supported` means established only for its recorded environment, operation, route and conditions; it does not prove permission or that a particular action succeeded. `unsupported` requires evidence of unavailability within those bounds. For example, deletion not exposed by the tested local tools describes that tool route, not universal impossibility of deletion. An untested route remains `unknown`. Descriptive effects, ownership, creation constraints and deletion scope also permit `unknown`; an empty field is not evidence of no effect.

For **each fact**, `capability_evidence_and_last_verified` identifies its source/retained observation or configured contract, exact applicability and limitations, who/what verified it and when, and the conditions requiring recheck. Retain exact evidence content or its content identity/locator, including the configuration revision for configured behavior, under the existing inventory history rules. Distinguish a documented/configured behavior from an observed result. Evidence for one field does not verify the whole profile. Keep prior observations when a fact changes; a later check must not silently universalize a bounded observation. A remembered behavior, another substrate's profile, or mere tool/UI existence is not verification.

Before selecting or relying on a substrate for a lifecycle operation, scheduling, recovery or cleanup, Foreman checks the required facts against the actual current environment/resource/route. A historical timestamp alone cannot establish continuing applicability. Changed configuration/target mode/route, contrary evidence, expired validity conditions or an unverified replacement context makes the affected fact stale or unknown for use. Verify through an authorized source/route before relying on it; if unavailable, keep that dependent action blocked. This rule does not authorize an experiment, destructive probe or unarchive. For deletion, unknown support or affected scope fails closed under the existing exact-scope authority rule above.

Capability, actual resource/task state and permission are three separate checks. A profile guides which owner/context/scheduler records must be queried during **Scheduler inventory and succession**; it does not mark a task live, prove a context reachable or deleted, establish message delivery/cessation, settle a receipt, or grant cleanup authority. Link actual operation/verification evidence in the existing attempt, scheduler and succession records. Keep archive, unarchive and permanent deletion distinct. The preceding conservative lifecycle/destructive rules remain controlling; a supported container-delete capability cannot enlarge generic worker-cleanup permission.

When selecting among permitted substrates, weigh setup, verification, cleanup and usage cost against required capabilities/isolation. This is qualitative selection guidance, not a topology rule or numeric duration threshold.

### Bounded evidence and acceptance cases

The two columns below illustrate representation of **historical reported observations**, not current operational profiles or platform guarantees. Sources: [local cases](https://github.com/davrec72/nested-planning-template/issues/27) and [local follow-up](https://github.com/davrec72/nested-planning-template/issues/27#issuecomment-5649922758); [TempTestProject1 report](https://github.com/davrec72/nested-planning-template/issues/27#issuecomment-5653656643). A real inventory must retain the exact resource IDs, evidence and applicability checks; these summaries supply no missing IDs or current verification.

| Fact | Tested local/ephemeral route | Tested ChatGPT Project/cloud Work route |
|---|---|---|
| Resource/creation | Recursive child creation observed. Bind each actual context and owning resource; do not infer identity from a Role name. | Cloud Work creation in disposable TempTestProject1 observed; initial local-target attempt rejected and created no task. This constraint is limited to that tested setup. |
| Archive/unarchive | Owner-child archive removed its recurring schedule in one case; unarchive did not recreate it. Ancestor archive left the descendant and its schedule intact in another case. | Archive, unarchive and their effects remain `unknown`: they were not tested by this report. |
| Deletion | Permanent deletion was not exposed by the tested local task tools: `unsupported` on that route; other routes remain `unknown`. | Work task deletion, then deletion of its verified empty disposable project, observed. Nonempty-container cascades and deletion scope outside that case remain `unknown`. |
| Scheduler support/owner | Child-owned recurring task operation observed; actual owner/task identity and current liveness still need their own evidence. | `unknown`; no schedules were created. Cloud creation/deletion does not establish scheduler behavior. |
| Reachability/routes | Archived history remained readable, but direct send to an archived target was rejected, not queued/delivered or auto-unarchived. These are different operations. | Task reply `got it` and rename from `Confirm receipt` to `TTPForeman` observed; after deletion the task was no longer readable. Archived-target behavior remains `unknown`. Rename can be retained as an additional scoped observation, not inferred from create support. |
| Evidence/currentness | Retain the reported cases and per-fact bounds; they do not establish today's support/state for a new context. | Retain the reported order: task removed, empty project removed, inventory count restored; no files/schedules created. It is not a reusable deletion authorization. |

| Acceptance case | Required conclusion |
|---|---|
| Two environments differ on archive/delete/scheduling | Separate profiles retain their own supported/unsupported/unknown facts. Logical Role/plan semantics do not change and neither profile fills the other's gaps. |
| A required capability is unknown, stale or contradicted | Block reliance until authorized verification resolves that fact for the actual target/route. Unaffected supported capabilities need their own checks; absence of an exposed tool proves only that bounded route limitation. |
| Container deletion is supported, but the proposed target contains other contexts or its scope is unknown | Expose the exact target/affected resource set or `unknown`; apply existing exact destructive authority. Worker-cleanup permission cannot authorize broader deletion, and unknown scope cannot be guessed from an empty-project test. |
| A successor finds an old profile and schedule ID | Revalidate applicability and query the recorded actual owner/task and routes under the existing succession procedure. Profile support is not liveness, a readable history is not a delivery route, and remembered UI behavior is not evidence. |
| A worker is unarchived or an ancestor is retired | Use the profile to identify the separate resource/scheduler queries; record actual outcomes. Do not manufacture restored tasks, descendant cleanup or receipt closure from the lifecycle label. |
| Capability verification itself is outside current authority | Leave the fact unknown and dependent action blocked; a profile requirement does not grant testing, creation or destructive permission. |

David's reported practical heuristic is that browser-heavy projects **probably** are not worthwhile for subprojects expected to take under about one hour unless a concrete capability/isolation need justifies them. This is non-normative owner guidance, not a platform limit or protocol threshold; the qualitative cost/benefit rule above remains the durable guidance.

Existing projects adopt these profile requirements under their preceding accepted governance. Populate profiles for current resources from bounded evidence, preserving unknowns and historical observations without fabricating prior checks. This adds runtime evidence inside the existing inventory; it changes no inventory identity/serialization/history, fence, receipt, grammar, authority or publication contract.

## Compatibility and migration

This contract leaves `plan-grammar-v2` and `plan-publication-v1` semantics unchanged. It adds an explicit execution contract and stricter operational records; adopting projects must approve/publish the change under their preceding accepted governance. It does not retroactively validate old packages or create temporary grants from a legacy `role` field.

First operational adoption chooses the initial inventory identity/locator, conditional mechanism, coordination domain and retention contract under prior authority. Reconcile complete legacy state into that initial baseline before managed dispatch is enabled; do not fabricate missing history. After adoption, the fixed-contract rule above prohibits same-version inventory/mechanism migration. Ordinary holder/claim and resource-ID succession inside the same domain remains supported; this section is not a provider/store migration framework.

Configure explicit `transition-action-v1` adoption before any operational Foreman dispatch/start/resume or obligation-creating revision/attempt/rebind/supersession. Its adopting transition carries the predecessor-approved legacy baseline; every later planning publication includes an approved manifest, including no-impact transitions. Under predecessor governance, prevent new obligation creation while identifying/reconciling the complete legacy set. After journaled adoption, index/reconcile the adopting event and all carried obligations and verify required checks before enabling execution. `none` remains no-dispatch until those conditions hold, even for an empty inventory. Existing authority, journal currentness and PlanRef/carrier-retention trust roots remain unchanged.

Fence adoption must itself be protected by a predecessor-valid mechanism when legacy execution is active or still dispatchable. Stop/reconcile and exclude further legacy dispatch, or obtain an explicitly authorized bounded one-time fence under prior authority; the candidate cannot supply its own authority. A first root/child publication may use explicit no-active-execution evidence only when no pre-existing dispatch-capable system exists. Historical events receive no invented fences.

To migrate an outstanding package:

1. Retain the original issued record. Translate an unambiguous `milestone: M` to `target_type: milestone`, `target_id: M` in a new revision. If both forms exist and conflict, stop the affected dispatch. Do not reinterpret that field as a Decision or parent Milestone.
2. Resolve exact target/authority/input records; obtain explicit bounded executor authorization, routes, checkpoints, and reserved decisions. A historical package with only `role` and scope has no inferred executor grant under this contract.
3. Inventory the existing attempt and independently verify its actual state, pending changes, results, and schedules. Do not redispatch it to populate the new form. Stop/recover unknown or insufficiently authorized execution and have the current authorized holder reissue as required.
4. Record the migration/adoption PlanRef and current validation evidence. Preserve unaffected evidence and historical grammar meanings. Unknown or incompatible target semantics require an explicit architecture/version decision, not silent translation.

See `examples/execution/CASES.md` for bounded protocol walkthroughs and counterexamples; they are not an operational plan or live scheduler evidence.
