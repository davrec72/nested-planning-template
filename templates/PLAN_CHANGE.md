# Plan change template

Use this for every semantic planning or Role change.

After explicit `qualified-reference-v1` adoption, fix this change record's repository/PlanID context and fully qualify every affected cross-plan object, Role or source under `planning/REFERENCES.md`. Bind external authority PlanRefs separately from the candidate's own baseline/candidate refs. Reference adoption/migration itself is an explicit semantic change; a proposed field does not activate it.

Candidate creation/approval, snapshot retention, publication-ref movement, trusted journal commit, and propagation are separate events. Follow `planning/PUBLICATION.md` and `planning/PUBLICATION_TRANSITIONS.md`.

```text
Semantic delta:
Affected milestones:
Affected roles:
Active work impact: none | continue | pause | redirect | supersede
Authority impact: none | binding change | scope change
Foreman dispatch required: yes | no
Controlling decision/evidence:
```

## Before the change

Resolve accepted state from the trusted publication journal:

```text
publication_ref:
publication_journal_high_water_event_id:
accepted_predecessor_commit:
prior_publication_id:
prior_plan_ref:
acting_role:
authority_source:
```

Do not use newest branch/ref content or candidate governance as accepted state.

## Candidate and approval

```text
candidate_plan_ref:
approval_event:
approved_by_role:
approval_authority_source:
approved_scope:
```

Approval binds the exact candidate. If content changes, obtain new approval.

For adopted `transition-action-v1` (or its predecessor-approved adoption baseline), complete the active-work analysis and prepare `templates/TRANSITION_ACTION.md` **before** approval. It belongs in the successor carrier, not necessarily the semantic candidate, and contains no own carrier SHA. Record:

```text
transition_action_contract: transition-action-v1
transition_action_path:
transition_action_record_id:
transition_action_blob_id:
execution_inventory_revision_or_snapshot:
publication_fence_id:
publication_fence_scope:
publication_fence_acquisition_and_held_through_commit_evidence:
legacy_reconciled_through_event_id: none | <predecessor high-water for adoption>
transition_action_approval_event:
```

Approval must bind the exact candidate and manifest blob/record identity under predecessor-valid authority. The same approval may cover both only if explicit; otherwise obtain a separate manifest approval. Rebuild/reapprove on changed candidate, manifest or affected inventory state under `planning/PUBLICATION_TRANSITIONS.md` section 9. A PR form is a review surface, not durable manifest storage.

## Candidate retention

```text
plan_snapshot_locator:
plan_snapshot_retention_evidence:
```

The exact candidate must be durably cold-fetchable independently of ordinary branch cleanup before publication.

## Active work handling

For adopted Decision/DATA activation changes, additionally identify:

```text
affected_node_and_contract_version:
exact_definition_and_input_revisions:
prior_operative_record: none | <exact result/resolution>
new_operative_record: none | <exact result/resolution>
replacement_revocation_or_withdrawal_record: <exact immutable record or none>
retained_record_history:
affected_branch_or_consumer_work_disposition:
```

The current accepted PlanRef is the sole operative selection boundary under `planning/NODE_CONTRACTS.md`. Retain prior records unchanged, validate exact incumbent replacement and authority, and give each affected work item an explicit bounded disposition. Do not publish an activation change while required disposition is unresolved or treat an unindexed result/resolution as current.

For Milestone status changes record:

```text
milestone_id:
prior_plan_ref:
prior_status_class:
new_status_class:
transition_evidence: <exact execution event, acceptance, or reopening decision>
transition_authority_source:
current_acceptance_record_index: none | <valid acceptance locator for DONE>
historical_acceptance_and_reopening_links: <locators or none>
```

Apply the transition-specific rules in `planning/CONVENTIONS.md`: projecting DONE requires valid acceptance/index; starting/resuming or pausing uses appropriate authorized execution evidence; reopening a DONE Milestone requires an authorized reopening/revocation/correction decision and preserves the old receipt unchanged. Reopening directly to INPROGRESS also needs start/resume evidence. Do not fabricate acceptance for a non-DONE status update or treat an unconfirmed stop as proved cessation.

For every affected active package state one:

```text
continue | pause | redirect | supersede
```

Identify exact package revisions/attempts from the configured execution inventory, affected typed targets, requested actions, recipient routes, and acknowledgement/application deadlines. Prepare recovery obligations under `planning/EXECUTION.md`; do not treat a missing worker as stopped.

The adopted manifest retains this exact impact baseline and a complete action/recipient/deadline/recovery payload for every affected attempt, including explicit `continue`. A checked no-impact publication still carries `active_work_impact: none` and `affected_attempts: []` plus a protected inventory baseline. Only first root/child publication with no pre-existing dispatch-capable system may use explicit no-active-execution evidence without a fence; legacy execution follows the predecessor-valid exclusion rules in section 9. Missing analysis is not no impact.

Until trusted publication succeeds, operational work remains governed by the prior accepted PlanRef.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

## Publication handoff

```text
transition_kind: bootstrap | normal | recovery
publication_ref:
accepted_predecessor_event_id:
accepted_predecessor_commit:
carrier_parent_commit:
successor_publication_id:
successor_carrier_commit:
prior_publication_id:
prior_plan_ref:
plan_ref: <candidate_plan_ref>
invalid_suffix_start: none | <commit>
invalid_suffix_tip: none | <commit>
```

For normal publication, actual carrier parent and accepted predecessor are the same. Recovery preserves an invalid/uncommitted actual suffix while using the last valid accepted predecessor for governance.

After applicable approvals and candidate retention, create the carrier containing CURRENT and the exact approved manifest/inputs. Conditionally acquire its preallocated durable fence against the exact analyzed inventory baseline using the same serialized mechanism as dispatch claims; mismatch requires rebuild/reapproval. Fence all affected obligation-creating/broadening mutations through ref movement, carrier/manifest retention and valid trusted journal commit. The event binds exact manifest and fence ID/scope/baseline/acquisition/continuity evidence; normal release follows commit. A plain reread is insufficient.

Before-ref abort must be durably verified before predecessor release. After ref movement, retention/journal failure leaves an uncommitted suffix and durable fence: keep it held through explicit recovery, or durably abort/reconcile the suffix before release. Any later publication after release needs fresh baseline/manifest/approval/fence. If commit succeeds but release fails, a successor validates the event and releases; timeout alone never clears it. Follow `planning/PUBLICATION_TRANSITIONS.md` section 9, including observation, no-impact, bootstrap and legacy rules.

## Publication evidence

```text
ref_update_receipt:
publication_journal_event_id:
journal_sequence:
```

The exact PlanRef becomes current only after the conditional ref movement succeeds **and** the trusted append-only/tamper-evident journal event commits.

## Foreman propagation payload

Only after journal commit send:

```text
publication_event_id:
publication_id:
publication_commit:
new_plan_ref:
prior_publication_id:
prior_plan_ref:
semantic_delta:
affected_roles:
affected_milestones:
active_work_impact:
authority_change:
controlling_links:
```

Foreman matches this payload to the exact trusted publication event and reconciles stale/duplicate/out-of-order events before applying transition-specific actions.

After journal commit, verify the exact journal-bound retained manifest and reconstruct/index each affected recipient/attempt request and receipt before its wake, using `templates/EXECUTION_RECEIPT.md`. Reuse its stable request/check identities and retain route history within the same receipt key. Record actual verified check IDs/owners for acknowledgement and application recovery. The publication reconciliation check must reconstruct every missing obligation from the manifest even if the initial Foreman notification is lost; only then may its marker advance. Historical pre-adoption obligations use the explicit reconciled adoption baseline, not invented manifests.

Track recorded, sent/wake attempted, delivered, acknowledged, applied, and closed separately. A sent/acknowledged pause remains **not confirmed stopped** until application/enforcement evidence covers its in-flight work. Preserve old receipts when a later change supersedes them; a new `continue` does not silently erase an unresolved stop.
