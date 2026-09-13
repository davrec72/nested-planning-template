# Reconstructing publication actions after a lost wake

These are bounded fictional source/protocol cases for `transition-action-v1`, not live publication, authority, scheduler or lifecycle experiments. Repeated-digit SHAs and all IDs/routes below are illustrative exact-identity tokens; they are not claims about real accepted commits. In the fixture, existing accepted publication, execution, Role authority and retained evidence are valid. The adjunct was already adopted before E1.

## One complete affected-attempt manifest

E1/P1 is the prior accepted event/PlanRef; P1 is `1111111111111111111111111111111111111111`. Candidate P2 is `2222222222222222222222222222222222222222`. A finite independent commit P2 exists before this manifest. It reduces the permitted test scope while `WP-TEST/r1/T1` runs. Stable record TA2, publication PUB2, journal event E2 and approval AP2 IDs are preallocated. The inventory mechanism holds claim L7 so no affected attempt can appear outside snapshot I7 before ref movement. The inline snapshot/analysis below is retained with the manifest, not in a PR description.

```json
{
  "transition_action_contract": "transition-action-v1",
  "transition_action_record_id": "TA2",
  "plan_id": "FIXTURE",
  "publication_event_id": "E2",
  "publication_id": "PUB2",
  "accepted_predecessor_event_id": "E1",
  "prior_plan_ref": "1111111111111111111111111111111111111111",
  "candidate_plan_ref": "2222222222222222222222222222222222222222",
  "semantic_delta": "Restrict the accepted test scope; pause the existing test attempt pending authorized revalidation.",
  "execution_contract": "planning/EXECUTION.md at P1",
  "execution_inventory_revision_or_snapshot": "I7",
  "inventory_baseline_evidence": {
    "revision": "I7",
    "claim": "L7 held from impact analysis through ref movement under P1 inventory policy",
    "outstanding_attempts": ["WP-TEST/r1/T1"],
    "outstanding_prior_requests": [],
    "other_active_work": [],
    "analysis": "T1 is the entire outstanding set and is affected by this restriction; no omitted continue or unresolved legacy obligation."
  },
  "legacy_reconciled_through_event_id": "none",
  "active_work_impact": "explicit",
  "no_impact_basis": "none",
  "action_authority_source": "Lead's existing scope-restriction authority in P1/ROLES and AUTH-1",
  "transition_action_approval_event": "AP2",
  "affected_attempts": [{
    "work_package_id": "WP-TEST",
    "package_revision": "r1",
    "attempt_id": "T1",
    "authorization_id": "AUTH-1 at P1",
    "target_type": "milestone",
    "target_id": "M-TEST",
    "target_record": "M-TEST definition at P1",
    "disposition": "pause",
    "exact_affected_scope": "All further test actions and in-flight test tools covered by AUTH-1",
    "action_authority_source": "Lead's existing scope-restriction authority in P1/ROLES and AUTH-1",
    "recipient_obligations": [{
      "request_id": "Q2",
      "requested_action": "pause",
      "requested_action_payload": "Start no further test segment; perform AUTH-1 safe stop; preserve output and report any in-flight tools and unstopped scope.",
      "obligated_recipient_identity_context": "Tester/context-T",
      "recipient_action_scope": "The exact affected test scope of T1",
      "initial_preferred_routes_or_resolution_rule": {"direct": "route-T", "fallback": "query-T"},
      "acknowledgement_deadline_rule": "E2.committed_at + 1 minute",
      "application_deadline_rule": "Q2 exact recipient acknowledgement time + 2 minutes",
      "recovery_check_obligations": [
        {"logical_id": "Q2-ACK", "owner": "Foreman under current accepted binding", "trigger": "acknowledgement deadline", "action": "query, authorized retry/fallback, escalate unresolved request", "verification": "actual scheduler task/owner/trigger evidence required"},
        {"logical_id": "Q2-APPLY", "owner": "Foreman under current accepted binding", "trigger": "application deadline or reported inability to apply", "action": "query in-flight effects and escalate unresolved stop", "verification": "actual scheduler task/owner/trigger evidence required"}
      ],
      "retry_query_fallback_escalation": "Query route-T/query-T and actual test effects; retry only supported authorized wakes; escalate to Lead/route-Lead if unreachable or not stopped. Preserve original deadlines and verify the next unresolved check.",
      "supersedes_request": "none"
    }]
  }]
}
```

The local IDs above inherit FIXTURE's accepted repository/plan context and expected field kind. Cross-plan uses require full qualified references and separate authority revisions. Full referenced P1/AUTH-1 authority, target, execution bounds and source evidence are retained under the existing accepted-record rules; the example does not grant them.

## Finite approval and carrier order

1. Finalize TA2 and compute its Git blob identity B-TA2. TA2 contains AP2's preallocated ID, not an approval hash and not its own blob/carrier hash.
2. The existing authorized holder issues durable AP2 binding exact P2 and B-TA2/TA2 under P1 authority. A candidate-only approval is insufficient. Retain AP2's verifiable evidence with the carrier or trusted journal under the existing approval trust rules, without requiring a later PR/comment lookup.
3. Retain P2. Create carrier R2 with CURRENT naming P2 and `planning/TRANSITION_ACTION.md` containing exactly B-TA2. No containing SHA needs to be known inside TA2; R2's SHA is learned after creation.
4. With I7 still covered by L7, advance the publication ref conditionally from accepted R1 to R2. Retain R2/tree/CURRENT/TA2 and required parent evidence under the existing carrier-retention contract.
5. Commit E2 with the exact successful ref-update evidence, R2 and P2 retention evidence, `transition_action_contract: transition-action-v1`, canonical path, B-TA2, TA2 and inventory-validation evidence binding I7/L7 to the manifest. Only now is P2 current. E2's event/publication/predecessor identities match TA2 and CURRENT.

The approval record and carrier can both be created in ordinary finite steps. A mutable PR, comment or worker context is not required to recover TA2's action payload.

## Lost wake and partial replay

| Observation | Required state and action |
|---|---|
| E2 commits at 12:00; the Foreman wake is lost before any request is created | P2 is current; no claim that T1 stopped. E2 and retained R2/TA2 remain discoverable from the trusted journal. |
| Verified publication reconciliation runs at 12:02 with marker E1 | Fetch R2 through its retained evidence, verify B-TA2 at the configured path, AP2/P1 authority, I7 completeness/serialization, and exact E1/P1/P2/E2 identities. |
| TA2 validates; current worker route is unavailable and the mutable inventory no longer lists T1 | Reconstruct/index Q2 for the exact Tester/context-T + WP-TEST/r1/T1 key from TA2. Missing current state is not absence of the obligation or evidence of cessation. |
| Q2 is indexed, then Foreman crashes before check reconciliation | Marker remains E1. Successor finds the same Q2/key and retains its history; create/reconcile only missing Q2-ACK/Q2-APPLY checks, using actual state before replacing a possibly live task. |
| Q2-ACK was due 12:01; discovery happens at 12:02 | Preserve 12:01 as overdue and perform immediate authorized recovery. Do not create a new one-minute window based on discovery time. |
| Direct route rejects; fallback reaches the same Tester/context-T | Append both transport observations to the same receipt. Route failure is not a second receipt obligation. |
| Exact acknowledgement at 12:03 reports a draining tool | Record acknowledgement and application due 12:05. T1 is still not confirmed stopped; actual application check remains required. |
| Every TA2 obligation and required check is indexed/reconciled and verified | Advance reconciliation marker to E2, independently of still-outstanding application. Q2 does not close merely because E2 was inventoried. |
| A required scheduler verification fails | Keep marker E1 with partial progress retained, block affected dependent work and escalate. Neither a logical check ID nor a future intention is proof of a live check. |
| Exact application evidence later accounts for all in-flight test work | Update the same receipt's application and reconcile closure/check disposition; failed direct-route history remains retained. |

A duplicate E2 wake does not create Q3, another receipt for the same key, or a second executable dispatch. A different independently obligated coordinator has its own recipient entry/receipt; a relay that only forwards Q2 does not.

## Approval, completeness, empty impact and retention counterexamples

| Case | Required result |
|---|---|
| Approval names P2 but not B-TA2/TA2 | Manifest is not approved; obtain explicit predecessor-valid approval before publication. |
| TA2 changes after AP2, even if the record ID is reused | Blob mismatch invalidates that approval; rebuild/reapprove before ref movement. |
| A new affected attempt T2 appears before final inventory check | Rebuild impact analysis, manifest and approval/carrier before publication. Old I7 cannot silently omit T2. |
| No execution inventory is adopted and no active execution exists | Explicit empty manifest with `execution_contract: none`, inventory `none`, `active_work_impact: none`, `affected_attempts: []` and exact no-active-execution basis; still approved/retained/bound. |
| Adopted inventory I8 is analyzed and no attempt is affected | Approved explicit empty manifest retains I8/no-impact analysis. Foreman can validate E3 and advance without receipts. |
| An affected T1 is deliberately grandfathered into P3 | List T1 explicitly with `disposition: continue`, exact recipient/action/payload/deadline/recovery rules. Do not encode it as empty impact. |
| Ref moved to R2 but retaining the carrier/manifest fails, or E2 cannot commit | R2 is uncommitted suffix state; E1/P1 remains accepted. Recover under prior governance and preserve the suffix evidence. TA2 is not operative merely because it exists. |
| Journal says B-TA2, but the retained path contains another blob or record ID | Fail closed. A PR copy, newer same-path manifest or plausible notification does not repair the mismatch. |
| Divergent recovery later displaces accepted R2 from live-ref reachability | Existing carrier retention still retrieves R2/TA2 for cold replay. Retain the recovery carrier/manifest and required invalid suffix separately; no new journal or retention trust root. |
| Recovery republishes P2 without changing semantic content | Still include an explicit approved recovery manifest with current analyzed impact/no-impact basis; equality of PlanRefs does not remove the adjunct requirement. |

## Legacy and bootstrap boundaries

An existing project's E0..E5 pre-adoption publications remain valid under their original governance. Before adopting in E6, reconcile legacy obligations through E5 under already-valid authority; retain exact inventory baseline I6 and any outstanding carry-forward obligations in TA6. TA6 records `legacy_reconciled_through_event_id: E5`, predecessor E5 and its PlanRef, and candidate P6. Predecessor-valid approval binds P6/TA6 before E6 publishes, so proposed P6 rules do not approve themselves.

If a legacy stop cannot be resolved or precisely carried forward, adoption/dependent work stays blocked; do not invent an E4 manifest. A precisely identified outstanding stop can be explicitly carried into TA6 with its predecessor relation and recovery obligations without claiming the worker stopped. A cold successor validates old journal history under old rules, then uses TA6's approved baseline and later exact manifests. Later records use legacy marker `none`.

A new root or child may adopt at first publication under its bounded founding/accepted-parent bootstrap authority. Prepare/approve an explicit empty/baseline manifest with predecessor and legacy fields `none`, include it in the first carrier and bind it in the first journal event. This does not create founder authority for an already initialized project or bypass the parent boundary.

These checks are schema/order/reconstruction walkthroughs. They do not demonstrate actual scheduling, ref-update receipts, authority signatures, transport delivery or physical cessation.
