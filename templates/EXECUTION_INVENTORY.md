# Execution inventory template

An instantiated project creates this inventory at the locator configured in its accepted `planning/EXECUTION.md`, or uses an explicitly configured equivalent. This index contains runtime coordination facts, not new planning authority. Keep issued package revisions, historical attempts/receipts, and results retrievable.

## Inventory and recovery identity

```text
project: <existing project/repository identity>
plan_id: <PlanID>
configuration_plan_ref: <accepted revision configuring this inventory>
inventory_revision: <serialized current revision/event>
coordination_claim: <current Foreman binding and exclusive mutation/dispatch claim evidence>
prior_claim_disposition: <released/fenced/other proven disposition>
last_reconciled_publication_event: <journal event through which all required requests are indexed>
current_checked_plan_ref: <exact current accepted PlanRef>
publication_reconciliation_check: <logical check ID below>
recovery_escalation_route: <configured authority and fallback route>
```

Do not advance the reconciliation marker merely because a message was sent. Per-attempt application remains separate below. Use the configured serialization mechanism for claims and updates; retain uncertain mutation outcomes for reconciliation.

## Package index

Every package is discoverable here, including drafts and dispatches with uncertain outcomes. Exact detailed records may be linked to keep the table short.

| Package ID / immutable revision | Exact package and authorization | PlanRef / typed target | Attempt / executor context | Coordination state / last execution observation | Return Role / route | Outstanding receipts / checks | Latest durable result |
|---|---|---|---|---|---|---|---|
| `<ID/revision>` | `<locators>` | `<PlanRef; type; ID; target record; parent bindings if any>` | `<attempt ID; identity; context; route>` | `<state; observation time/evidence>` | `<Role; durable destination; wake/query route>` | `<IDs/locators or none>` | `<exact artifact/revision or none>` |

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
last_applied_publication_event:
outstanding_material_receipts:
scheduled_check_ids:
latest_durable_result_and_exact_revision:
predecessor_or_replacement_attempt_and_disposition:
next_recovery_action_owner_and_due_time:
```

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

Record the recovering Foreman binding, inventory/claim revision, current publication evidence, packages queried, schedules verified/recreated, results recovered, unresolved attempts/receipts, and next real checks. Follow the ordered procedure in `planning/EXECUTION.md` before resuming coordination or authorizing any replacement dispatch.
