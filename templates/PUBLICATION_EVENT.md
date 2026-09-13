# Publication journal event

Use this schema for one committed `plan-publication-v1` event in the configured trusted publication journal.

```text
event_id: <stable unique ID>
sequence: <monotonic journal sequence>
transition_kind: bootstrap | normal | recovery
plan_id: <PlanID>
publication_protocol: plan-publication-v1
publication_ref: <configured ref>
ref_update_receipt: <durable host/journal evidence of successful exact old->new ref movement>
carrier_parent_commit: <actual Git parent of successor carrier or none>
accepted_predecessor_commit: <last accepted carrier or none>
accepted_predecessor_event_id: <last accepted event or none>
accepted_predecessor_carrier_evidence_locator: <prior event's retained carrier locator or none>
successor_carrier_commit: <exact carrier now associated with this event>
carrier_evidence_locator: <durable cold-fetchable exact carrier/tree/CURRENT/required-parent evidence>
carrier_evidence_retention_evidence: <evidence under configured carrier-retention contract>
publication_id: <CURRENT publication_id>
prior_publication_id: <previous accepted publication ID or none>
prior_plan_ref: <previous accepted PlanRef or none>
plan_ref: <new/current accepted PlanRef>
plan_snapshot_locator: <durable cold-fetchable semantic snapshot>
plan_snapshot_retention_evidence: <evidence under configured PlanRef-retention contract>
invalid_suffix_start: none | <first quarantined commit>
invalid_suffix_tip: none | <actual invalid/uncommitted tip>
invalid_suffix_evidence_locator: none | <cold-fetchable retained suffix evidence>
invalid_suffix_retention_evidence: none | <evidence under configured carrier-retention contract>
approval_event: <durable approval locator>
publication_authority_source: <accepted source>
publisher_identity: <attributable identity>
committed_at: <timestamp or durable event time>
```

## Required properties

For adopted `transition-action-v1` publications, including the predecessor-approved adoption baseline, also record:

```text
transition_action_contract: transition-action-v1
transition_action_path: <configured path in exact successor carrier tree>
transition_action_blob_id: <exact Git blob identity at that path>
transition_action_record_id: <manifest record ID>
transition_action_inventory_validation_evidence: <exact analyzed baseline/obligation set and fence proof bound to this manifest>
publication_fence_id: <preallocated stable ID or none only under the permitted bootstrap exception>
publication_fence_scope: <exact protected coordination domain/scope or explicit bootstrap no-active basis>
publication_fence_baseline: <same exact analyzed inventory revision/snapshot as the manifest; or permitted none>
publication_fence_acquisition_evidence: <durable conditional acquisition against that baseline; or permitted bootstrap basis>
publication_fence_held_through_commit_evidence: <durable cold-verifiable continuity through this valid journal commit; or permitted bootstrap basis>
```

Validate these against the retained carrier and exact approved manifest under `planning/PUBLICATION_TRANSITIONS.md` section 9. Every adopted bootstrap/normal/recovery planning event includes them, even for explicit no impact. Pre-adoption historical events retain their original requirements; do not invent bindings for them.

Acquisition/continuity proof comes from the same configured serialized inventory/dispatch mechanism under existing trust rules, not a last-second reread. The event binds the preallocated fence identity and actual durable evidence; it does not require post-commit evidence inside the approved manifest or its own event hash. Normal release follows valid commit. Crash, failed retention/journal or failed release follows section 9's durable recovery rules; a lease/timeout cannot erase a fence.

- The journal itself is append-only/tamper-evident under the trust basis fixed at bootstrap or an authorized later migration.
- A cold reader can enumerate committed events in order and identify the high-water event.
- `ref_update_receipt` is evidence from the configured hosting/journal trust mechanism, not merely a self-authored sentence in the carrier.
- `plan_snapshot_locator` retrieves the exact `plan_ref` independently of ordinary work branches.
- `carrier_evidence_locator` retrieves the exact accepted successor carrier plus its tree, exact `planning/CURRENT.md`, and every Git object required to perform protocol-mandated carrier checks.
- Carrier evidence remains fetchable for at least the publication-journal lifetime even if the accepted carrier is displaced from live-ref reachability by later divergent recovery.
- When the adjunct applies, that evidence includes the exact bound manifest and reconstruction inputs; missing/mismatched path/blob/record, approval or inventory evidence fails closed. No PR or notification substitutes for retained content.
- Normal events use the same actual and accepted predecessor carrier and link to the retained predecessor carrier evidence through the prior event.
- Recovery events may have a different actual Git predecessor and accepted predecessor. They must retain the quarantined invalid suffix evidence and explicitly link the separately retained accepted predecessor carrier evidence.
- A recovery event is not valid if garbage collection, ref movement, or branch cleanup could erase either the displaced accepted carrier evidence or the invalid suffix evidence required for cold validation.
- Missing journal, semantic snapshot, carrier, or required invalid-suffix evidence fails closed for dependent execution.
