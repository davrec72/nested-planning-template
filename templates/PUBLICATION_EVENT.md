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
successor_carrier_commit: <exact carrier now associated with this event>
publication_id: <CURRENT publication_id>
prior_publication_id: <previous accepted publication ID or none>
prior_plan_ref: <previous accepted PlanRef or none>
plan_ref: <new/current accepted PlanRef>
plan_snapshot_locator: <durable cold-fetchable snapshot>
plan_snapshot_retention_evidence: <evidence under configured retention contract>
invalid_suffix_start: none | <first quarantined commit>
invalid_suffix_tip: none | <actual invalid/uncommitted tip>
approval_event: <durable approval locator>
publication_authority_source: <accepted source>
publisher_identity: <attributable identity>
committed_at: <timestamp or durable event time>
```

## Required properties

- The journal itself is append-only/tamper-evident under the trust basis fixed at bootstrap or an authorized later migration.
- A cold reader can enumerate committed events in order and identify the high-water event.
- `ref_update_receipt` is evidence from the configured hosting/journal trust mechanism, not merely a self-authored sentence in the carrier.
- `plan_snapshot_locator` must retrieve the exact `plan_ref` independently of ordinary work branches.
- Normal events use the same actual and accepted predecessor carrier.
- Recovery events may have a different actual Git predecessor and accepted predecessor; the invalid suffix remains preserved but non-accepted.
- Missing journal or snapshot evidence fails closed for dependent execution.
