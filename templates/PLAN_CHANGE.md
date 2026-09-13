# Plan change template

Use this for every semantic planning or Role change.

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
