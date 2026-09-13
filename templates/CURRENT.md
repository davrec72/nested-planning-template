# Current accepted plan publication

Instantiate this file as `planning/CURRENT.md` on the configured publication ref.

Do not leave placeholders in an operational project.

```text
publication_protocol: plan-publication-v1
transition_kind: bootstrap | normal | recovery
publication_id: <stable unique ID>
plan_id: <PlanID>
grammar: <grammar declared by plan_ref>
plan_ref: <exact accepted planning commit SHA>
plan_snapshot_locator: <durable cold-fetchable locator>
plan_snapshot_retention_evidence: <durable evidence under configured retention contract>
carrier_parent_commit: <actual Git parent of this carrier or none>
accepted_predecessor_commit: <last accepted publication carrier or none>
accepted_predecessor_event_id: <trusted journal event ID or none>
prior_publication_id: <previous accepted publication ID or none>
prior_plan_ref: <previous accepted PlanRef or none>
invalid_suffix_start: none | <first quarantined commit>
invalid_suffix_tip: none | <actual invalid/uncommitted tip>
approval_basis: role | founding | parent
approval_event: <durable locator proving approval of plan_ref>
approved_by_role: <RoleID or none>
approval_authority_source: <accepted source or none>
founding_record: <durable locator or none>
parent_authority_source: <durable locator or none>
publisher_identity: <attributable identity>
publication_authority_source: <source authorizing publication/recovery>
publication_journal_event_id: <trusted journal event ID>
published_at: <timestamp or durable event time>
```

## Interpretation

- `plan_ref` is the accepted semantic planning snapshot; the carrier commit is not automatically the PlanRef.
- Every published `plan_ref` must remain cold-fetchable through `plan_snapshot_locator` independently of ordinary branch cleanup/rebase/squash.
- `publication_journal_event_id` must resolve in the configured trusted append-only/tamper-evident publication journal.
- For `normal`, `carrier_parent_commit == accepted_predecessor_commit`, and the accepted predecessor fields match the latest valid journal event.
- For `recovery`, `carrier_parent_commit` is the actual bad/uncommitted Git tip while `accepted_predecessor_commit` remains the last valid accepted carrier. The invalid suffix is preserved but not accepted.
- `bootstrap` has no accepted predecessor and is valid only under the explicit founding/parent bootstrap contract.
- Candidate governance changes do not validate the transition that makes themselves current; predecessor accepted governance controls.
- Fields that do not apply use `none`.

Cold validation starts from the configured trusted publication journal and verifies carrier/ref state and retained snapshots under `planning/PUBLICATION_TRANSITIONS.md`. Git ancestry or CURRENT predecessor claims alone are not enough to establish historical ref movements.
