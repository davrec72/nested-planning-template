## Plan publication transition

Use this checklist for one `plan-publication-v1` bootstrap, normal, or recovery publication.

A semantic PR/merge is not the publication event. Accepted publication requires a durable retained PlanRef, durable retained carrier evidence, a successful exact ref movement, and a committed trusted journal event.

`transition_action_contract: none` is planning/no-autonomous-dispatch mode under [operational eligibility](../../planning/PUBLICATION.md#operational-execution-eligibility), even with an empty inventory. A material publication remaining in that mode must affect no active/outstanding execution obligation. Legacy obligations require valid prior-authorized stop/reconciliation or conforming adoption; no guessed action payload substitutes. To enable managed execution, adopt `transition-action-v1` and reconcile/index the adopting event and carried obligations with checks verified before dispatch. First root/child publication follows the same choice: `none` stays no-dispatch; v1 needs its accepted/reconciled baseline.

## Trusted publication baseline

```text
publication_ref:
publication_journal_kind:
publication_journal_locator:
publication_journal_high_water_event_id:
accepted_predecessor_commit:
accepted_predecessor_event_id:
accepted_predecessor_carrier_evidence_locator:
prior_publication_id:
prior_plan_ref:
plan_snapshot_retention_kind:
carrier_evidence_retention_kind:
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

The exact candidate must already be cold-fetchable under the configured PlanRef-retention contract.

## Successor carrier

For `transition-action-v1`, including its approved adoption baseline, prepare the [manifest](../../templates/TRANSITION_ACTION.md) after the exact candidate and before predecessor-valid approval. Record:

```text
transition_action_contract: none | transition-action-v1
prior_transition_action_contract:
adoption_baseline_reconciliation_and_eligibility_evidence:
transition_action_path:
transition_action_blob_id:
transition_action_record_id:
transition_action_approval_event:
execution_inventory_revision_or_snapshot:
transition_action_inventory_validation_evidence:
publication_fence_id:
publication_fence_scope:
publication_fence_baseline:
publication_fence_acquisition_evidence:
publication_fence_held_through_commit_evidence:
legacy_reconciled_through_event_id:
```

Approval binds candidate plus exact manifest, or separate predecessor-valid approval binds the manifest. Every adopted bootstrap/normal/recovery publication has one, including checked empty impact; affected `continue` is explicit. No own carrier SHA belongs in the manifest. It and its reconstruction inputs are included in the carrier below and retained under the existing carrier contract. After approval, conditionally acquire the named durable fence against the exact analyzed baseline through the same serialized inventory/dispatch mechanism before ref movement. Changed baseline requires rebuild/reapproval. Block affected obligation-creating/broadening mutations through valid journal commit, including no-impact transitions with adopted inventory; a plain reread is insufficient. Use section 9's explicit bootstrap/legacy basis where applicable.

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

## Retained carrier evidence

Before the journal event can commit, record and verify:

```text
carrier_evidence_locator:
carrier_evidence_retention_evidence:
accepted_predecessor_carrier_evidence_locator:
invalid_suffix_evidence_locator: none | <locator>
invalid_suffix_retention_evidence: none | <evidence>
```

The successor carrier evidence must retrieve the exact commit/tree/CURRENT and parent evidence needed by the protocol. Recovery must preserve both the quarantined invalid suffix and the separately retained displaced accepted predecessor chain, even if neither remains reachable from the future live-ref tip.

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
- [ ] Execution eligibility is explicit: no-dispatch under `none`, or current accepted v1 plus valid adopting/legacy baseline; autonomous dispatch remains blocked until baseline obligations are indexed/reconciled and checks verified.
- [ ] An applicable manifest has predecessor-valid approval binding its exact blob/record ID and complete serialized inventory analysis; no-impact and legacy baseline claims are evidenced.
- [ ] Manifest ID/scope/baseline match the durable conditional fence acquisition and held-through-valid-commit evidence; every affected dispatch/mutation path uses the same serialization.
- [ ] Abort/recovery/release disposition is durable under section 9; no timeout or holder loss clears a fence.
- [ ] The exact candidate is durably retained and cold-fetchable independently of ordinary branches.
- [ ] Bootstrap trust configuration includes publication ref, journal, PlanRef-retention, and carrier-evidence-retention contracts.
- [ ] Transition validation uses predecessor accepted governance; candidate governance does not validate itself.
- [ ] For normal transition, successor carrier Git parent equals the last accepted carrier.
- [ ] For recovery, successor carrier Git parent equals the actual bad/uncommitted ref tip, while accepted predecessor fields name the last valid accepted carrier/event.
- [ ] Recovery explicitly records the quarantined invalid suffix and uses authority valid under the last accepted PlanRef.
- [ ] The publication ref update is conditional/non-force from the exact expected actual ref object.
- [ ] A durable trusted `ref_update_receipt` records the successful old->new movement.
- [ ] Exact successor-carrier evidence is retained before journal acceptance and remains cold-fetchable for the journal lifetime.
- [ ] For the adjunct, retained carrier evidence includes the exact manifest/inputs and the journal binds its path/blob/record ID plus inventory-validation evidence; a missing/mismatched manifest fails closed.
- [ ] The accepted predecessor carrier chain remains separately retrievable even after divergent recovery displaces it from live-ref reachability.
- [ ] Recovery retains the invalid suffix evidence required for every protocol-mandated cold check.
- [ ] A trusted journal event is committed only after successful ref movement and all required semantic/carrier retention evidence exists; until then any advanced carrier is uncommitted state.
- [ ] Journal sequence/high-water remains append-only/tamper-evident under the configured trust contract.
- [ ] Replay/reset/divergence is detected by disagreement with trusted journal history rather than Git ancestry alone.
- [ ] The propagation payload binds the exact committed publication journal event and carrier.

## After successful journal commit

Only after the trusted event commits does the event's `plan_ref` become current accepted planning state.

Normal fence release occurs durably after valid commit; subsequent dispatch validates successor current state and outstanding obligations. Commit success with release failure keeps the scope blocked until successor verification/release. Before-ref failure requires verified abort before release; post-ref retention/journal failure keeps the fence through explicit recovery or durable abort/suffix reconciliation before predecessor release. Later publication after release needs fresh baseline/manifest/approval/fence. See `planning/PUBLICATION_TRANSITIONS.md` section 9.

Then Foreman may apply the transition-bound semantic delta. Candidate merge/staging, ref movement alone, or message arrival is not sufficient.

For adopted events, Foreman validates the exact retained manifest and indexes/reconciles every missing request/recipient receipt/check before advancing its publication-reconciliation marker. This works without the original wake or PR history. A valid empty manifest advances without receipts; historical pre-adoption events use the explicit legacy adoption boundary under `planning/PUBLICATION_TRANSITIONS.md` section 9.
