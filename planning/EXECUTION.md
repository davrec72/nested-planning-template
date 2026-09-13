# Work execution and recovery

This is the shared Foreman–executor contract for typed packages, temporary executor authorization, material-change receipts, and durable recovery. It supplements the accepted roadmap grammar; it does not change node classes, prerequisite satisfaction, Role delegation, or the publication protocol.

This template source is not an operational execution inventory. An instantiated project adopts/configures this contract through its normal accepted publication process before using it.

## Configuration and durable records

The accepted project configuration in this file must identify:

```text
execution_inventory_locator: planning/EXECUTION_INVENTORY.md
inventory_write_policy: <authorized writer, serialized update/claim mechanism, history retention>
publication_reconciliation_interval: <finite maximum interval>
receipt_ack_timeout: <finite interval>
receipt_apply_timeout: <finite interval after acknowledgement>
recovery_escalation_route: <Role and reachable fallback route>
```

Replace placeholders before operational dispatch. An accepted configuration may select an exact alternate inventory locator, such as an issue index. A branch, chat memory, or worker's unindexed report cannot silently replace that configured inventory.

The inventory is authoritative for **coordination state**, not for planning authority. Foreman may update runtime records under accepted coordination permissions without publishing a new PlanRef for every check. Preserve exact package revisions, prior attempts, requests/receipts, results, and state-change evidence in recoverable history. Serialize inventory changes and dispatch claims through the configured mechanism (for example, conditional versioned updates that reject a stale inventory revision); a pre-write read alone is insufficient. A claim binds its ID, inventory revision, current holder/binding and prior claim disposition. Check the current claim before each dispatch or other coordination mutation; stale holders/claims must fail. If a claim/update has an unknown outcome, reconcile it before retrying.

Use `templates/EXECUTION_INVENTORY.md`, `templates/WORK_PACKAGE.md`, and `templates/EXECUTION_RECEIPT.md`. An equivalent representation must preserve all required fields and transitions. Discover the full outstanding set from the configured inventory, including prepared/dispatched attempts, material receipts, and schedules; do not require knowledge of old chat IDs to discover it.

Every record is project/plan-qualified using the existing plan identity rules. Local package IDs, Role names, and schedule IDs alone are not globally unique. This requirement does not create cross-project authority.

## Typed targets

Every package binds `target_type` and `target_id` at its exact accepted `plan_ref`:

| `target_type` | `target_id` resolves to | Dispatch and return boundary |
|---|---|---|
| `milestone` | An existing Milestone | Its own prerequisites and contract govern execution. Return evidence to the named substantive authority; delivery does not accept it. |
| `decision` | An existing Decision | Its own prerequisites and authorized research/review scope govern preparation. `return_to` is its unique deciding Role; evidence is not that Role's judgment. |
| `data` | An existing DATA node | Its own dependency/evidence contract and accepted producing scope govern work. Producing an artifact does not establish satisfaction beyond the accepted node rules. |
| `plan-maintenance` | A stable bounded maintenance scope in an accepted record named by `target_record` | The accepted scope names its authority, inputs, and limits. This is a work classification, not a new roadmap node or exemption from governance. |

Record `target_record` for every type so the exact definition can be retrieved. No target type supplies authority by itself. Do not assign Roles to Gates, invent Milestones for activities, or infer Decision/DATA activation rules from this table. Use the current accepted `CONVENTIONS.md` for those rules; unresolved semantics block only the dependent action.

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

An unrelated new PlanRef does not force restart. Reconcile publication history, record the current checked PlanRef/event and why the original package/authorization remains valid. Preserve its original revision and evidence. A changed permitted scope, target meaning, reserved decision, or input contract requires a new authorized package revision; do not edit an issued grant in place.

## Dispatch and attempts

Separate the stable package ID, immutable `package_revision`, and per-executor `attempt_id`. The inventory contains one current dispatch claim for each package, binding its exact revision and attempt. A new revision or supersession label cannot bypass reconciliation of its predecessor's execution. Multiple intentional parallel assignments require separate bounded packages; retries are not extra authority.

Before sending work:

1. Validate current publication/retention/authority, typed target prerequisites, authorization, executor route, and exact input revisions.
2. Serialize a durable claim containing the package/revision, attempt ID, executor/return routes, current authorization, state `dispatch-pending`, and recovery obligation. Create and verify a real scheduled check whenever any dispatch acknowledgement, return, or future condition will be asynchronous; persist its ID, owner, trigger, and evidence before dispatch.
3. Send the exact package/revision and attempt ID. Record each transport attempt and its observed outcome. An ambiguous send leaves `dispatch-pending`/unknown execution, not permission to create another attempt.
4. The executor acknowledges the exact assignment and starts only after validation. It deduplicates repeat delivery of that attempt, returning current state or existing results instead of starting again. Foreman records `running` only with executor/start evidence.

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

There are two required recovery loops:

- **Publication to Foreman:** maintain a verified scheduled reconciliation at the configured maximum interval. Compare the trusted journal high-water mark to a durable `last_reconciled_publication_event`, enumerate affected attempts, and create any missing material requests even when no notification arrived. Advance that reconciliation marker only after all required requests/obligations are durably indexed. This is separate from each attempt's last applied event.
- **Foreman to executor:** before relying on a material request, schedule and verify its acknowledgement/application checks, indexed to that receipt. Foreman owns timeout handling: retry an authorized supported wake route, query the executor/effects, use a known fallback route, and escalate to the configured authority if still unresolved. Acknowledgement without application still needs its application deadline and recovery check. Failed scheduling is `ACTION NEEDED`; an unscheduled future intention is not recovery.

While a material authority/scope restriction remains unapplied, Foreman blocks new dependent dispatch, replacement execution, resumption, and final readiness/acceptance handoffs. Preserve unaffected work. Report the affected attempt as **not confirmed stopped**, including the exposure interval and last verified action. A timeout or unavailable worker is not evidence that it stopped.

Each executor revalidates current publication/authority and outstanding requests at the package's bounded execution checkpoints, as well as before new/resumed substantive work and final handoff. If it cannot validate, it starts no further segment and follows its preauthorized safe-stop procedure. A non-interruptible action must have an explicit bounded duration/effect and stop procedure before it starts. This bounds cooperative operation; messaging alone cannot instantly halt already-running effects or an unreachable worker.

Projects needing stronger guarantees may require fail-closed leases/heartbeats and external fencing. Such a policy must define expiry, renewal authority, enforcement point, clock/failure assumptions, and proof of effect cessation. An unenforced lease timestamp is not a fence. If the configured stop bound cannot be met, do not dispatch that work under a best-effort assumption.

Reconcile publication-driven requests in trusted journal order. Keep `last_reconciled_publication_event` separate from `last_applied_publication_event` per attempt. Duplicate applied requests are no-ops; stale requests cannot undo a later valid application. A later `continue` cannot erase an unresolved earlier stop: validate the intervening history and explicit disposition of that stop, then obtain valid reauthorization before resumption. Preserve old requests and link any superseding applied receipt.

## Scheduler inventory and succession

Inventory every publication watch, package check, receipt retry/application check, and cleanup obligation. Each needs a stable logical check ID, package/receipt relation or explicit plan-wide purpose, scheduler/task ID, concrete execution owner/context, target route, exact trigger/cadence/time zone, action/prompt locator, last verified state/time/evidence, next due time, and replacement/cleanup disposition. Record context reachability separately from task liveness.

On startup, succession, or capability loss:

1. Validate current accepted publication state and locate the configured inventory. Acquire the serialized coordination/dispatch claim under current Foreman binding before making mutations; a prior holder cannot continue using an obsolete claim.
2. Reconstruct each nonterminal package revision/attempt, executor route, authorization, last applied event, material receipt, exact result, and check. Preserve historical records. Mark unsupported old liveness claims `unknown`.
3. Query actual executor and scheduler state through available read-only routes. Reconcile results and in-flight effects before any dispatch retry or replacement. A durable result may settle a returned package even when its old executor is unreachable; absence of a result cannot prove non-execution.
4. Classify each outstanding check as `verified-live`, `recreated`, `completed`, or `lost/cancelled`, with evidence. If verification is unavailable, retain `unknown` as an unresolved blocker; do not force it into a proven class. Recreate a missing check only after resolving an old possibly live check or ensuring duplicate wakeups are harmless and idempotent. Index the replacement ID/owner and disposition of the old one. Follow-up checks must reconcile before dispatching, so a duplicated wake never authorizes duplicated execution.
5. Reconcile journal gaps and outstanding receipts, restore verified future checks, and revalidate active authorizations. Resume coordination of the existing attempt when valid; do not issue a fresh executor merely because the Foreman changed.
6. If replacement execution is necessary, prove the prior attempt terminal/not started or effectively fenced; record that evidence, its results/effects, a linked new attempt and current authorization. Otherwise preserve `unknown`/`pause-requested`, schedule recovery if possible, and escalate. Never trade missing state for speculative redispatch.

Schedule lifecycle depends on the execution substrate. Do not infer that archive equals deletion, that an ancestor's retirement removes descendant work, or that unarchiving restores schedules. Verify the actual context/resource owner and each task's state. A task ID or a UI card without an existence/status result is not liveness proof.

Externalize results, inventory, and recovery routes before a planned holder teardown. Cleanup disposition is an independently evidenced fact, not a side effect inferred from retirement. Generic worker cleanup permission does not authorize destroying a multi-context project/container; exact destructive scope needs its own authority. This contract does not define a universal execution-context capability profile or topology.

## Compatibility and migration

This contract leaves `plan-grammar-v2` and `plan-publication-v1` semantics unchanged. It adds an explicit execution contract and stricter operational records; adopting projects must approve/publish the change under their preceding accepted governance. It does not retroactively validate old packages or create temporary grants from a legacy `role` field.

To migrate an outstanding package:

1. Retain the original issued record. Translate an unambiguous `milestone: M` to `target_type: milestone`, `target_id: M` in a new revision. If both forms exist and conflict, stop the affected dispatch. Do not reinterpret that field as a Decision or parent Milestone.
2. Resolve exact target/authority/input records; obtain explicit bounded executor authorization, routes, checkpoints, and reserved decisions. A historical package with only `role` and scope has no inferred executor grant under this contract.
3. Inventory the existing attempt and independently verify its actual state, pending changes, results, and schedules. Do not redispatch it to populate the new form. Stop/recover unknown or insufficiently authorized execution and have the current authorized holder reissue as required.
4. Record the migration/adoption PlanRef and current validation evidence. Preserve unaffected evidence and historical grammar meanings. Unknown or incompatible target semantics require an explicit architecture/version decision, not silent translation.

See `examples/execution/CASES.md` for bounded protocol walkthroughs and counterexamples; they are not an operational plan or live scheduler evidence.
