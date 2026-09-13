# Execution inventory template

First operational adoption creates/configures this inventory, or an explicitly chosen initial representation, under accepted `planning/EXECUTION.md` and the complete legacy/adoption baseline rules. Its logical locator/identity, serialization mechanism, coordination domain and history contract are then fixed for that PlanID/execution-contract lifetime; no later same-version store move or silent fallback is supported. This index contains runtime coordination facts, not new planning authority. Keep issued package revisions, historical attempts/receipts, and results retrievable.

## Inventory and recovery identity

```text
project: <existing project/repository identity>
plan_id: <PlanID>
configuration_plan_ref: <accepted revision configuring this inventory>
fixed_inventory_contract: <exact adopted logical locator/identity, serialization, domain and retention bindings in EXECUTION.md>
inventory_revision: <serialized current revision/event>
coordination_claim: <current Foreman binding and exclusive mutation/dispatch claim evidence>
prior_claim_disposition: <released/fenced/other proven disposition>
last_reconciled_publication_event: <journal event through which all required requests are indexed>
current_checked_plan_ref: <exact current accepted PlanRef>
publication_reconciliation_check: <logical check ID below>
recovery_escalation_route: <configured authority and fallback route>
```

For operationally adopted execution, validate fixed-contract continuity from adoption before using this inventory. An unavailable/contradictory mechanism fails closed; similar rows in another store are insufficient. Current writer/Foreman authority and claim are separate mutable facts, validated at use. Keep ordinary row/revision/fence lifecycles and authorized holder/claim, credential/session/route and scheduler-ID changes inside the same configured mechanism, retaining old/new evidence. Same-contract provider upgrades require proof of preserved conditional-serialization/history semantics; see `planning/EXECUTION.md`.

Do not advance the reconciliation marker merely because a message was sent. Per-attempt application remains separate below. Use the configured serialization mechanism for claims and updates; retain uncertain mutation outcomes for reconciliation.

For `transition-action-v1`, retain per-event reconciliation evidence: exact journal-bound carrier manifest path/blob/record ID, validated inventory baseline/approval and fence acquisition/continuity proof, every manifest request/recipient obligation and logical check, partial reconstruction progress and actual verification evidence. Advance only after the complete set is indexed/reconciled with required checks verified. Preserve a validated explicit empty manifest and its protected baseline as the no-receipt reason; affected `continue` entries are not empty. Follow `planning/EXECUTION.md` for replay and the predecessor-reconciled legacy adoption baseline.

## Durable publication fences

Index every active/uncertain fence and retain its history in the **same serialized mechanism** as inventory/dispatch claims. Succession must discover these without knowing the prior publisher/context. Each record retains:

```text
publication_fence_id:
publication_fence_scope_and_coordination_domain:
analyzed_inventory_revision_or_snapshot_and_exact_obligation_set:
candidate_manifest_blob_record_and_publication_event_identities:
accepted_predecessor_and_configured_mechanism_authority:
conditional_acquisition_outcome_and_evidence:
current_fence_state: acquisition-unknown | acquisition-failed | held | release-unknown | released
held_through_commit_evidence_and_allowed_nonbroadening_mutation_history:
ref_update_outcome_and_retention_journal_state:
abort_or_recovery_authority_and_exact_transition_associations:
release_basis_outcome_and_evidence:
recovery_owner_route_and_next_check:
```

Acquisition is conditional against the manifest's exact approved baseline; mismatch stops publication and requires rebuild/reapproval. All affected dispatch/start/resume/new revisions/attempts/executor or recipient rebindings and other obligation-creating/broadening mutations check this current fence within the same serialization. A pre-read, old claim or scheduler wake cannot bypass it. Observations/obligation-reducing evidence may be recorded only if they cannot broaden obligations; retain that classification.

Hold through valid trusted journal commit. Record normal release afterward and validate successor state for new dispatch. Pre-ref abort needs verified non-publication before release. Post-ref retention/journal failure keeps the fence durable until explicit recovery while held, or durable abort and suffix reconciliation before predecessor release; any later publication after release needs fresh baseline/manifest/approval/fence. Successful journal commit plus failed release remains conservatively blocked until a successor validates and releases. Unknown outcomes, timeout/lease expiry and holder loss cannot erase fences. See `planning/PUBLICATION_TRANSITIONS.md` section 9; this index is neither a second currentness journal nor proof that in-flight work stopped.

## Execution-context capability profiles

Keep one profile per actual environment/context and applicability scope under `planning/EXECUTION.md` -> **Execution-context capability profiles**. Detailed records may be linked from this inventory. Use existing project/plan qualification, serialized updates and retained history; profiles neither replace the inventory nor grant permissions. Bind package attempts and scheduler rows to the applicable exact profile revision.

```text
profile_id_and_revision: <durable local profile identity/revision>
context_identity_and_locator: <provider/environment; actual resource ID and retrievable locator, or unknown>
container_identity_and_relation: <actual containing resource ID/locator and relation, none with evidence, or unknown>
profile_applicability: <exact environment/configuration/tool surface/routes/target modes and limits>
route_limitations: <operation-specific read/send/recovery routes and constraints or unknown>
associated_attempts_and_scheduler_records: <exact inventory record links or none with evidence>
context_kind: <actual substrate/context kind or unknown>
create_supported: supported | unsupported | unknown
creation_constraints_or_target_modes: <bounded modes/conditions or unknown>
archive_supported: supported | unsupported | unknown
unarchive_supported: supported | unsupported | unknown
permanent_delete_supported: supported | unsupported | unknown
child_creation_supported: supported | unsupported | unknown
scheduled_task_supported: supported | unsupported | unknown
schedule_owner: <actual owning resource/context, scheduler/task record links and ownership relation; or unknown>
archive_effect_on_own_schedules: <scoped observed/configured effect or unknown>
archive_effect_on_descendants: <scoped archive/retirement effect and descendant resource relation or unknown>
unarchive_effect_on_schedules: <scoped observed/configured effect or unknown>
archived_target_reachability_or_delivery_behavior: <operation/route-specific read/send limitations or unknown>
project_or_container_delete_supported: supported | unsupported | unknown
deletion_scope: <operation and exact target/affected resource set/limits, or unknown>
capability_evidence_and_last_verified: <per-fact evidence records below>
prior_profile_and_change_evidence: <retained prior revision and reason, or none for first record>
```

For each fact retain source/evidence identity and locator, observed versus configured basis, exact environment/resource/operation/route tested, scope/limitations, verifier and verification time/event, and validity/recheck conditions with the current applicability conclusion. Unknown/stale facts remain explicit; a timestamp or verified create capability cannot validate other fields. Record unsupported only within the evidenced bounds, not as a universal product claim. Additional scoped facts such as rename support may use the same evidence structure without implying any untested capability.

Actual context reachability/lifecycle outcomes, task liveness and operation/cleanup results stay in the linked attempt, scheduler and succession records, separate from capability support. A profile can identify what to query but cannot supply a current state result. Before relying on required facts, check their continuing applicability or perform authorized verification; unresolved deletion support/scope blocks deletion, and capability evidence supplies no destructive authority.

## Package index

Every package is discoverable here, including drafts and dispatches with uncertain outcomes. Exact detailed records may be linked to keep the table short.

| Package ID / immutable revision | Exact package and authorization | Package baseline PlanRef / typed target | Attempt / executor context | Coordination state / last execution observation | Return Role / route | Outstanding receipts / checks | Latest durable result |
|---|---|---|---|---|---|---|---|
| `<ID/revision>` | `<locators>` | `<immutable package PlanRef; type; ID; definition at that ref; parent bindings if any>` | `<attempt ID; identity; context; route>` | `<state; observation time/evidence>` | `<Role; durable destination; wake/query route>` | `<IDs/locators or none>` | `<exact artifact/revision or none>` |

Each linked attempt record must retain:

```text
attempt_id:
package_id_and_revision:
authorization_id_and_authorizing_role_binding:
dispatch_claim_and_transport_attempts:
executor_identity_context_and_routes:
return_role_and_routes:
coordination_state_and_transition_evidence:
execution_observation_and_in_flight_effects:
executor_context_reachability_checked_at_and_evidence:
current_checked_plan_ref_and_publication_event:
current_validation_evidence_and_conclusion:
last_applied_publication_event:
outstanding_material_receipts:
scheduled_check_ids:
latest_durable_result_and_exact_revision:
predecessor_or_replacement_attempt_and_disposition:
next_recovery_action_owner_and_due_time:
```

Before first dispatch, every resume or other obligation-creating action, retain that exact current accepted SHA/event and reconciliation/current-sensitive check evidence under `planning/EXECUTION.md` -> **Package baseline and current validation**. Preserve prior checks in history. Neither the inventory-wide checked ref nor the immutable package baseline substitutes for this attempt's action-time check. An unrelated later PlanRef does not rewrite the package `plan_ref` or its target definition.

`unknown`, `blocked`, and `pause-requested` do not prove cessation. `returned` does not mean accepted. A replacement needs prior cessation/non-start or effective fencing evidence, not just a new row.

## Material request index

Use one receipt per request + affected recipient identity/context + exact package revision/attempt. Within this project/plan, index `request_id`, `recipient_identity_context`, `work_package_id`, `package_revision`, and `attempt_id`; do not add a row/receipt merely for another route to the same recipient/attempt. Retain closed/superseded records and all transport-attempt history, including failed routes.

| Request / receipt | Exact source and package revision / attempt | Obligated recipient identity/context | Requested action | Transport-attempt history / delivery evidence | Acknowledged evidence | Applied evidence / stopped scope | Ack/apply deadlines and recovery checks | Closure / supersession |
|---|---|---|---|---|---|---|---|---|
| `<IDs/locator>` | `<publication event or valid stop authority; package/revision/attempt>` | `<identity/context>` | `<action>` | `<routes, destinations, times and observations/locators or unknown>` | `<receipt or none>` | `<receipt or not confirmed stopped>` | `<absolute deadlines; actual check IDs>` | `<open or evidence/linked successor>` |

An independently obligated different recipient/context or package revision/attempt gets a separate receipt. This includes a nested coordinator with its own acknowledgement/application duty, but not a mere transit hop. Close on reconciled obligation/application or explicit valid supersession, not on every route succeeding; failed route history is retained without becoming a second outstanding obligation. A separate receipt does not automatically settle the earlier one.

## Scheduler index

Include plan-wide publication reconciliation, package follow-ups, receipt retries/application checks, and cleanup obligations. Each scheduled resource has its own owner and verification evidence.

| Logical check / purpose / related record | Scheduler / actual task ID | Owner context / target route | Trigger / cadence / time zone / next due | Exact action or prompt locator | Last verification / evidence | Reconciliation state | Replacement / cleanup disposition |
|---|---|---|---|---|---|---|---|
| `<ID; package/receipt or plan-wide purpose>` | `<scheduler locator; task ID>` | `<concrete owner; target>` | `<condition/time; next due>` | `<exact durable instructions>` | `<checked at; evidence>` | `<unknown / verified-live / recreated / completed / lost/cancelled>` | `<old/new IDs and proof>` |

`recreated` includes proof that the new task is live. `completed` includes result/fulfilled obligation evidence. `lost/cancelled` does not settle an outstanding work obligation: recreate or escalate it. If the old check may still run, reconcile it or make duplicate wakeups idempotent before recreating. A follow-up queries this inventory before any dispatch.

Track context reachability and schedule existence separately. Archive, unarchive, retirement, deletion, or a remembered task ID is not a scheduler verification. Preserve exact owner, old ID and cleanup result when replacing a schedule.

## Succession/reconciliation log

Record the recovering Foreman binding, inventory/claim revision, current publication evidence, active/uncertain fence reconstruction and disposition, packages queried, schedules verified/recreated, results recovered, unresolved attempts/receipts, and next real checks. Follow the ordered procedure in `planning/EXECUTION.md` before resuming coordination or authorizing any replacement dispatch.
