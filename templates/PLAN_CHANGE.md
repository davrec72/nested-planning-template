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

After journal commit, record/index one material request/receipt per affected attempt before its wake, using `templates/EXECUTION_RECEIPT.md`. Record actual verified check IDs/owners for acknowledgement and application recovery. The publication reconciliation check must discover this event even if the initial Foreman notification is lost.

Track recorded, sent/wake attempted, delivered, acknowledged, applied, and closed separately. A sent/acknowledged pause remains **not confirmed stopped** until application/enforcement evidence covers its in-flight work. Preserve old receipts when a later change supersedes them; a new `continue` does not silently erase an unresolved stop.
