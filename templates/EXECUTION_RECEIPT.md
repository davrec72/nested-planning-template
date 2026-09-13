# Material execution request and receipt template

Use with `planning/EXECUTION.md`. Record the request durably before attempting a wake. One receipt is keyed by request + affected recipient identity/context + exact package revision/attempt, even when a plan change fans out to many workers. Within its project/plan context, the key fields are `request_id`, `recipient_identity_context`, `work_package_id`, `package_revision`, and `attempt_id`; routes are not identity fields.

## Request identity and authority

```text
request_id: <stable ID>
receipt_id: <stable ID for this exact request/recipient/package-revision/attempt key>
project: <existing project/repository identity>
plan_id: <PlanID>
work_package_id:
package_revision:
attempt_id:
authorization_id:
requested_action: continue | pause | revoke | reduce-scope | redirect | supersede
requested_action_payload: <exact instructions/destination/changed bounds when needed>
exact_affected_scope:
recipient_identity_context:
recipient_route: <initial/preferred locator; not part of the receipt key>
recorded_at:
supersedes_request: <exact request or none>
```

For a published change include the full validated transition binding:

```text
publication_event_id:
publication_id:
publication_commit:
new_plan_ref:
prior_publication_id:
prior_plan_ref:
semantic_delta:
active_work_impact:
validated_journal_and_retained_carrier_evidence:
transition_action_path_blob_and_record_id: <verified source for an adopted publication>
transition_action_recipient_obligation: <exact manifest attempt/recipient entry; stable request ID>
```

For `transition-action-v1`, reconstruct the exact action payload and anchored deadlines from that event's retained manifest under `planning/EXECUTION.md`. Reuse the manifest request ID and receipt key on replay; do not reset expired deadlines, derive actions from notification prose or split one recipient obligation by transport route. A historical pre-adoption request retains its original evidence and any explicit adoption-baseline linkage.

For a stop under existing revocation terms instead record the exact authorization/term, current issuing Role/holder binding, independent authority source, checked PlanRef, and durable stop record. Such a stop restricts execution; it cannot change accepted planning state or authorize resumption.

## Transport attempts

Direct, fallback, retry, webhook and prompt routes to the same obligated recipient/context and package revision/attempt append transport history inside this receipt. Retain failed/rejected/unknown attempts when another route succeeds. If the obligated recipient/context or work attempt changes, use a different receipt; a transit hop alone creates no new recipient obligation.

| Transport attempt / time | Route / observed destination | Sent or wake attempted | Transport outcome / delivery evidence |
|---|---|---|---|
| `<ID/time>` | `<supported route/context>` | `<observed fact>` | `<delivered / rejected / unknown; exact evidence>` |

Sending or waking does not prove delivery, acknowledgement, or application. A rejected route remains undelivered. If transport exposes no delivery confirmation, leave it unknown until recipient evidence establishes receipt.

## Recipient acknowledgement

```text
acknowledged_at: <time or none>
acknowledging_identity_context:
matched_request_package_revision_attempt:
validated_authority_or_publication_evidence:
understood_action_and_scope:
can_apply: yes | no | partly
limitations_and_expected_application_time:
acknowledgement_evidence: <durable exact locator>
```

Acknowledgement is not proof of stopping. A rejected/invalid request is a recorded response, not a successful application; escalate contradictory authority.

## Applied result

```text
applied_at: <time or none>
applied_by_or_enforcement_authority:
exact_action_and_scope_applied:
last_action_revision_and_side_effects:
in_flight_tools_jobs_and_disposition:
remaining_unstopped_scope: <explicit list or none with evidence>
application_evidence: <durable receipt or verified enforcement proof>
last_applied_publication_event: <when publication-driven>
```

Until the exact requested stop is evidenced, report **not confirmed stopped** for unresolved execution. Partial cessation is partial application; keep remaining scope outstanding. Preserve evidence of work that ran after the restriction became effective.

## Recovery and closure

```text
Foreman_owner_and_route:
acknowledgement_due_at:
application_due_at:
deadline_rules_and_anchor_evidence: <retain manifest rules/resolved anchors for adopted publications>
actual_verified_check_ids_owners_and_triggers:
retry_query_fallback_and_escalation_route:
latest_recovery_observation_and_next_action:
closure: open | applied-and-reconciled | superseded
closure_evidence_or_validated_successor_receipt:
remaining_obligations_and_schedule_disposition:
```

Do not close on send, timeout, inaccessible executor, or an unrelated later message. Supersession requires explicit validated disposition and linkage; it cannot erase an unresolved stop or manufacture permission to resume. Reconcile publication requests in journal order and keep the inventory's reconciliation marker distinct from the attempt's application marker.

Closure reconciles this recipient's requested obligation (or explicit valid supersession), not success of every route. A failed route remains history, not a separate outstanding receipt once this obligation is satisfied through another route. An independently obligated nested coordinator has its own receipt; a mere forwarding hop does not. Neither that separate receipt nor a new recipient/attempt automatically settles this one.
