## Plan publication transition

Use this checklist for one `plan-publication-v1` bootstrap, normal, or recovery publication.

A semantic PR/merge is not the publication event. Accepted publication requires a durable retained PlanRef, a successful exact ref movement, and a committed trusted journal event.

## Trusted publication baseline

```text
publication_ref:
publication_journal_kind:
publication_journal_locator:
publication_journal_high_water_event_id:
accepted_predecessor_commit:
accepted_predecessor_event_id:
prior_publication_id:
prior_plan_ref:
plan_snapshot_retention_kind:
```

These values must come from the bootstrap-fixed or authorized migrated trust contract, not unpublished candidate governance.

## Candidate being published

```text
candidate_plan_ref:
plan_snapshot_locator:
plan_snapshot_retention_evidence:
plan_id:
grammar:
approval_basis: role | founding | parent
approval_event:
approved_by_role: <RoleID or none>
approval_authority_source: <accepted source or none>
founding_record: <locator or none>
parent_authority_source: <locator or none>
```

The exact candidate must already be cold-fetchable under the configured retention contract.

## Successor carrier

```text
transition_kind: bootstrap | normal | recovery
successor_carrier_commit:
carrier_parent_commit:
accepted_predecessor_commit:
accepted_predecessor_event_id:
CURRENT.prior_publication_id:
CURRENT.prior_plan_ref:
invalid_suffix_start: none | <commit>
invalid_suffix_tip: none | <commit>
```

For `normal`, actual Git parent and accepted predecessor are identical. For `recovery`, Git parent is the actual invalid/uncommitted tip while accepted predecessor remains the last valid carrier.

## Publication actor and ref movement

```text
publisher_identity:
publication_authority_source:
expected_old_ref_object:
new_ref_object: <successor_carrier_commit>
ref_update_receipt:
```

Repository write access alone is not publication authority.

## Trusted journal event

```text
publication_journal_event_id:
journal_sequence:
ref_update_receipt:
committed_at:
```

The event must satisfy `templates/PUBLICATION_EVENT.md` and be durably committed to the configured trusted append-only/tamper-evident journal.

## Validation checklist

- [ ] Candidate approval binds the exact `candidate_plan_ref` under already-valid governance.
- [ ] The exact candidate is durably retained and cold-fetchable independently of ordinary branches.
- [ ] Bootstrap trust configuration includes publication ref, journal, and PlanRef-retention contracts.
- [ ] Transition validation uses predecessor accepted governance; candidate governance does not validate itself.
- [ ] For normal transition, successor carrier Git parent equals the last accepted carrier.
- [ ] For recovery, successor carrier Git parent equals the actual bad/uncommitted ref tip, while accepted predecessor fields name the last valid accepted carrier/event.
- [ ] Recovery explicitly records the quarantined invalid suffix and uses authority valid under the last accepted PlanRef.
- [ ] The publication ref update is conditional/non-force from the exact expected actual ref object.
- [ ] A durable trusted `ref_update_receipt` records the successful old->new movement.
- [ ] A trusted journal event is committed after the successful ref movement; until then any advanced carrier is uncommitted state.
- [ ] Journal sequence/high-water remains append-only/tamper-evident under the configured trust contract.
- [ ] Replay/reset/divergence is detected by disagreement with trusted journal history rather than Git ancestry alone.
- [ ] The propagation payload binds the exact committed publication journal event and carrier.

## After successful journal commit

Only after the trusted event commits does the event's `plan_ref` become current accepted planning state.

Then Foreman may apply the transition-bound semantic delta. Candidate merge/staging, ref movement alone, or message arrival is not sufficient.
