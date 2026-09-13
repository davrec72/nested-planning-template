# Reconstructing publication actions after a lost wake

These are bounded fictional source/protocol cases for `transition-action-v1`, not live publication, authority, scheduler or lifecycle experiments. Repeated-digit SHAs and all IDs/routes below are illustrative exact-identity tokens; they are not claims about real accepted commits. In the fixture, existing accepted publication, execution, Role authority and retained evidence are valid. The adjunct was already adopted before E1.

## One complete affected-attempt manifest

E1/P1 is the prior accepted event/PlanRef; P1 is `1111111111111111111111111111111111111111`. Candidate P2 is `2222222222222222222222222222222222222222`. A finite independent commit P2 exists before this manifest. It reduces the permitted test scope while `WP-TEST/r1/T1` runs. Stable record TA2, publication PUB2, journal event E2, approval AP2 and publication fence F2 IDs are preallocated. Snapshot I7 is analyzed under P1's accepted serialized inventory/dispatch mechanism. After approval, conditional F2 acquisition must protect that exact baseline through valid E2 commit; a plain I7 read is insufficient. The inline snapshot/analysis below is retained with the manifest, not in a PR description.

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
  "publication_fence_id": "F2",
  "publication_fence_scope": {"coordination_domain": "FIXTURE serialized execution inventory/dispatch mechanism", "scope": "All existing or potential test execution affected by P2 scope restriction", "guarded_mutations": ["dispatch", "start", "resume", "new package revision/attempt", "executor/recipient rebind", "other obligation-creating/broadening mutation"]},
  "inventory_baseline_evidence": {
    "revision": "I7",
    "mechanism": "P1 configured conditional inventory/fence mechanism; acquisition must match I7 and exact obligation set",
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
4. Conditionally acquire F2 against I7 and its exact obligation set through that same serialized mechanism; changed baseline fails acquisition and requires rebuild/reapproval. Record actual acquisition A-F2 bound to F2/scope/I7/P2/TA2/B-TA2/E2, with a durable release guard and history proving continuity through valid commit. With F2 held, advance the publication ref conditionally from accepted R1 to R2. Retain R2/tree/CURRENT/TA2 and required parent evidence; the fence still excludes all affected obligation-creating mutations.
5. While F2 remains held, commit E2 with exact ref-update and R2/P2 retention evidence, manifest contract/path/B-TA2/TA2 and inventory-validation evidence binding I7's obligation set. Journal fields `publication_fence_id: F2`, scope, `publication_fence_baseline: I7`, A-F2 acquisition and held-through-commit evidence validate under the configured guard/history; a claim that F2 stayed held is insufficient. Only now is P2 current. Event/publication/predecessor identities match TA2 and CURRENT.
6. Durably release F2 only after valid E2 commit. Every subsequent dispatch validates P2 and outstanding transition obligations. If release fails, a successor verifies E2 and performs the release; it cannot infer release from timeout.

The approval record and carrier can both be created in ordinary finite steps. A mutable PR, comment or worker context is not required to recover TA2's action payload.

## Lost wake and partial replay

| Observation | Required state and action |
|---|---|
| E2 commits at 12:00; the Foreman wake is lost before any request is created | P2 is current; no claim that T1 stopped. E2 and retained R2/TA2 remain discoverable from the trusted journal. |
| Verified publication reconciliation runs at 12:02 with marker E1 | Fetch R2 through its retained evidence, verify B-TA2 at the configured path, AP2/P1 authority, I7 completeness and F2 acquisition/held-through-E2 proof, and exact E1/P1/P2/E2 identities. |
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
| T2 commits before conditional F2 acquisition | I7 acquisition fails; rebuild impact analysis/manifest/approval/carrier to include T2. See the exact interleaving regression below. |
| First root/child publication has no pre-existing dispatch-capable execution system | Explicit empty manifest with execution/inventory/fence `none`, `active_work_impact: none`, `affected_attempts: []` and exact no-active basis; still approved/retained/bound. |
| Adopted inventory I8 is analyzed and no attempt is affected | Approved explicit empty manifest retains I8/no-impact analysis; conditionally acquire its scoped fence and hold through valid E3 commit. Only after validating that proof may Foreman advance without receipts. |
| An affected T1 is deliberately grandfathered into P3 | List T1 explicitly with `disposition: continue`, exact recipient/action/payload/deadline/recovery rules. Do not encode it as empty impact. |
| Ref moved to R2 but retaining the carrier/manifest fails, or E2 cannot commit | R2 is uncommitted suffix state; E1/P1 remains accepted and F2 stays held. Explicit recovery while held, or durable abort/suffix reconciliation before predecessor release, is required. TA2 is not operative merely because it exists. |
| Journal says B-TA2, but the retained path contains another blob or record ID | Fail closed. A PR copy, newer same-path manifest or plausible notification does not repair the mismatch. |
| Divergent recovery later displaces accepted R2 from live-ref reachability | Existing carrier retention still retrieves R2/TA2 for cold replay. Retain the recovery carrier/manifest and required invalid suffix separately; no new journal or retention trust root. |
| Recovery republishes P2 without changing semantic content | Still include an explicit approved recovery manifest with current analyzed impact/no-impact basis; equality of PlanRefs does not remove the adjunct requirement. |

## Legacy and bootstrap boundaries

An existing project's E0..E5 pre-adoption publications remain valid under their original governance. Before adopting in E6, reconcile legacy obligations through E5 under already-valid authority; retain exact inventory baseline I6 and any outstanding carry-forward obligations in TA6. TA6 records `legacy_reconciled_through_event_id: E5`, predecessor E5 and its PlanRef, and candidate P6. Predecessor-valid approval binds P6/TA6 before E6 publishes, so proposed P6 rules do not approve themselves.

Under the current eligibility rule, `none` blocks new managed dispatch/start/resume while that baseline is formed under prior authority. Even after valid E6 commit, managed execution remains ineligible until E6/TA6 and the complete carried obligations are durably indexed/reconciled with required checks verified. A lost adoption wake invokes the same exact retained-baseline replay; it does not authorize dispatch before that step. A precisely defined outstanding stop may be carried without claiming cessation, but unknown legacy scope/payload cannot be guessed.

If a legacy stop cannot be resolved or precisely carried forward, adoption/dependent work stays blocked; do not invent an E4 manifest. A precisely identified outstanding stop can be explicitly carried into TA6 with its predecessor relation and recovery obligations without claiming the worker stopped. A cold successor validates old journal history under old rules, then uses TA6's approved baseline and later exact manifests. If its marker is missing or predates adoption, reconstruct TA6's complete carried/adoption obligation set before advancing to E6; do not first demand an E4 manifest or skip unverified legacy obligations. Later records use legacy marker `none`.

A new root or child may adopt at first publication under its bounded founding/accepted-parent bootstrap authority. Prepare/approve an explicit empty/baseline manifest with predecessor and legacy fields `none`, include it in the first carrier and bind it in the first journal event. The fence may be omitted only with explicit proof of no pre-existing dispatch-capable execution system. An existing active/still-dispatchable legacy system requires predecessor-valid serialization/exclusion; otherwise stop/reconcile work and exclude new legacy dispatch, or establish a bounded one-time mechanism under prior authority. Candidate rules cannot authorize their own fence. No historical fences are fabricated. This does not create founder authority for an already initialized project or bypass the parent boundary.

These checks are schema/order/reconstruction walkthroughs. They do not demonstrate actual scheduling, ref-update receipts, authority signatures, transport delivery or physical cessation.

## I7/T2 interleaving regression

TA2/AP2 are final and approved over I7 for T1; P1 remains current until valid E2. T2 would be another affected test attempt, even though no T2 existed in I7. Fence scope therefore includes the test dispatch/start entry points and potential new test packages, not just T1's identity.

| Serialized order | Required outcome |
|---|---|
| Publisher merely rereads I7; T2 then commits I8 under P1; ref advances and E2 accepts old TA2 | This is the rejected race. A plain read gives no exclusion; the event lacks conforming acquisition/continuity proof and cannot validate. Replaying only T1 must not advance the marker. |
| T2 commits I8 before conditional F2 acquisition against I7 | Acquisition fails. No ref movement using AP2/TA2. Analyze I8 including T1/T2, build fresh immutable TA2b/AP2b/carrier and fence F2b, then conditionally acquire and publish. Lost-wake replay reconstructs both attempts' obligations. |
| Conditional F2 acquisition against I7 commits first | T2's current serialized fence check blocks dispatch/start through ref movement, retention and valid E2 commit. After durable release, T2 must validate P2 and its outstanding transition obligations; P1's removed scope cannot authorize it. Lost-wake replay of TA2 omits no crossing attempt. |
| T2 prepared a dispatch claim before F2, but has not sent/started | Its pending claim must be in the baseline analysis if it creates an affected obligation. Its later send/start still checks the current fence through the same mechanism and blocks. A prior claim/read does not bypass F2. |
| F2 protects only T1, leaving the affected new-package entry point open | Reject incomplete scope before publication. Naming an existing attempt is not a complete coordination domain. |

## Fence failure, observation and compatibility cases

| Case | Required result |
|---|---|
| F2 acquisition outcome is unknown after a crash | Discover/reconcile its durable inventory record before dispatch or retry; do not create a speculative duplicate fence/attempt. |
| Publication fails before ref movement, and abort is durably verified | Verify the aborted attempt cannot later publish/commit, then release F2 to P1-governed execution. Unknown ref outcome cannot use this path. |
| Ref moved, retention/journal failed, recovery continues while F2 is held | Preserve suffix and continuous F2 scope. Under P1 authority bind exact recovery manifest/approval/transition identities and protected baseline to retained acquisition/history; release only after valid recovery journal commit. |
| Ref moved, transition instead aborts durably | Reconcile/classify the suffix under existing recovery rules before predecessor release. Do not treat the uncommitted carrier as accepted. |
| T2 appears after that abort/release and a later publication is attempted | New baseline must include T2; obtain fresh manifest/approval/fence. Old TA2/AP2 cannot survive release merely because candidate P2 is unchanged. |
| E2 commits, but release fails or the publisher disappears | P2 is current; F2 continues conservative blocking. Successor discovers it, verifies E2 and durably releases. This is a liveness failure, not permission to guess. |
| Fence lease/time limit expires while publication outcome is ambiguous | Keep the fence; timeout is not verified release or safe predecessor resumption. |
| T1 returns or provides cessation evidence while F2 is held | Record the observation/reduction through the same mechanism if it cannot broaden obligations. TA2 can conservatively retain T1; later reconciliation preserves its real evidence. |
| A purported acknowledgement also rebinds the executor or launches successor work | That is obligation-creating/broadening, not a pure observation; block it while fenced. |
| A scheduler wake or fallback route would start a new affected attempt | The same current fence guard blocks it; delivery mechanics do not bypass serialization. |
| Entirely unrelated work is provably outside F2's domain | It may continue under its own current authority; uncertainty about scope cannot be used to narrow the fence. |
| Empty adopted inventory was read before a new dispatch | No-impact still requires conditional acquisition and holding through commit. If the dispatch wins, rebuild; if the fence wins, block the dispatch. |
| First root/child claims no active work but a legacy dispatcher can still create it | No no-fence bootstrap exception. Use predecessor-valid exclusion/reconciliation; do not call dispatch capability empty inventory. |
| Legacy adoption proposes its only fencing authority inside candidate P6 | Reject self-authorized adoption. Prior authority must stop/reconcile and exclude dispatch or establish the bounded one-time mechanism first. |
| An older historical event lacks the newly adopted fence fields | Preserve its original semantics; do not fabricate proof or silently reinterpret the event. |
| Provider claims an atomic equivalent but supplies only a Git conditional update or inventory reread | Insufficient. Require predecessor-valid configured proof of no obligation-creating mutation from analyzed baseline through accepted journal commit, cold-reconstructible under existing trust rules. |
| Journal fence ID/scope/baseline mismatches the manifest, or continuity evidence is missing | Fail closed for event validation and lost-wake marker advancement. A current empty inventory cannot repair historical proof. |

All fixture outcomes are documentation-level reasoning. No real fence provider, concurrency implementation, scheduler, journal or lifecycle experiment was run; the adopting system must supply and verify the configured serialized mechanism and durable proof.

## Operational adoption eligibility regression

These symbolic cases apply the current eligibility rule; they do not retroactively label all historical pre-adoption execution invalid. `none` means no autonomous Foreman dispatch, even when an accepted inventory/Foreman binding exists. Commissioning read-only Decision research still creates a package/attempt obligation and needs accepted v1; merely reading the inventory does not.

| Current configuration and proposed action | Required outcome |
|---|---|
| `none`, no dispatch-capable execution/affected obligations; publish a planning-only change that keeps `none` | Permitted under valid planning/publication authority and no-impact evidence. Remains no-dispatch. |
| `none`, inventory exists but is empty; attempt the first managed dispatch | Blocked pending valid v1 adoption and baseline reconciliation. The first attempt cannot create its own eligibility. |
| `none`, read-only inventory query or status observation | Permitted within accepted coordination authority; it cannot dispatch/rebind/start an executor or manufacture action payloads. |
| `none`, commission a new read-only research worker or superseding attempt | Blocked: these create execution obligations, despite the proposed work being read-only or labeled replacement. |
| Legacy T1 is active/outstanding under `none`; propose material E2 scope reduction requiring pause without adoption | Block that execution-changing publication and new dispatch/resume. Do not accept a manifest-free E2 then guess its missing pause request. Use valid prior-authorized reconciliation/adoption or durable stop/reconciliation under valid legacy rules. |
| Legacy T1 exists, but a planning change provably does not affect its obligations and retains no-dispatch mode | May publish under valid prior authority and impact evidence; T1 is not guessed absent and managed dispatch stays blocked. |
| Proposed candidate adds v1 but the trusted journal still makes `none` current | No operational eligibility. Candidate existence, approval or merge does not adopt the contract. |
| Accepted v1 declaration names the wrong carrier path, or manifest/approval/legacy evidence is missing | Fail closed for affected execution; a declaration alone does not satisfy the gate. |
| Adopting event is validly committed but its carried requests/checks have not been indexed/verified | New PlanRef is current, but managed dispatch remains blocked. Finish exact baseline replay/reconciliation first. |
| Baseline is complete, but publication reconciliation has a failure blocking the proposed action | That action remains blocked. A past successful adoption is not permission to ignore a later failure. |
| All adoption/reconciliation checks pass, but a carried T1 pause is not applied | The general mode gate may pass; T1/dependent work still cannot resume or bypass outstanding material-stop rules. Indexed is not applied. |
| Legacy evidence cannot identify the full active/outstanding set or exact carry/stop/exclusion payloads | Adoption/enablement fails closed. Do not fabricate historical manifests, fences, recipients or pause requests. |
| First root/child accepted bootstrap chooses `none` | Valid no-dispatch bootstrap within its authority. Parent grant, Foreman binding or empty inventory does not authorize first execution. |
| First root/child intends execution and adopts v1 with valid empty/baseline manifest | First dispatch waits for accepted publication, valid baseline indexing/reconciliation and verified required checks, as well as ordinary authority/prerequisite/fence guards. |
| A provider or project labels an undefined contract "equivalent" | Not operationally supported. A future alternative needs explicit versioned journal-binding/completeness/fence/replay/adoption/failure semantics; a v1-compatible fence representation does not replace v1 adoption. |

## Lost adoption wake with carried legacy T1

This is a separate fixture from the already-adopted TA2 above. Assume E1/P1 is accepted under valid legacy rules with `transition_action_contract: none`, and T1 is a real outstanding legacy attempt. No new managed attempt is eligible under the current template. The existing authority can reconcile T1 and approve adoption; these symbolic references do not supply that authority.

| Order | Durable state / permitted action |
|---|---|
| 1. Form the baseline under predecessor governance | Exclude new obligation-creating dispatch/start/resume/revisions/attempts/rebindings. Reconcile legacy through E1 and identify T1's exact grant/scope/recipient, required pause action, original outstanding requests and bounded deadlines/recovery data. Account for every other obligation by carry, durable stop or explicit prior-authorized exclusion. Unknown scope blocks progress. |
| 2. Prepare P2 adoption and TA2 baseline | P2 explicitly adopts v1 at the configured path. TA2 records `legacy_reconciled_through_event_id: E1`, exact analyzed baseline, complete T1/Q2 payload and preallocated fence ID/scope. Prior authority approves exact candidate/manifest; acquire/hold the fence under existing section 9 rules. No candidate self-authorization. |
| 3. Publish valid E2 | Retain candidate and carrier/manifest, commit trusted event with exact identities/fence proof, then durably release as permitted. P2 is accepted. Dispatch remains blocked until baseline reconciliation; release alone does not enable it. |
| 4. Adoption wake is lost | The verified scheduled publication-reconciliation check discovers E2 after marker E1. It validates E1 legacy coverage and E2's exact retained TA2, authority/approval/fence proof, and complete carried T1 obligations. No PR history or invented E1 manifest is needed. |
| 5. Reconstruct/index T1/Q2 and checks | Reuse TA2's stable request/recipient/attempt/check identities and anchored deadlines. Preserve any pre-existing evidence; create only missing records, verify actual checks and retain partial progress after a crash. Failed checks leave enablement blocked. |
| 6. Complete adopting-event reconciliation | Only after every carried/adoption obligation is indexed/reconciled with required checks verified may the marker advance and the general operational eligibility gate pass. T1 is still not confirmed stopped without application evidence. |
| 7. Consider new work or T1 resumption | Independently validate current configuration/path, authority, target/ancestor prerequisites, fence and outstanding publication actions. Unaffected authorized work may proceed; T1/dependents remain blocked while its material pause is unapplied. No duplicate T1 dispatch is created to populate the new inventory. |

These cases add eligibility to the existing manifest/fence/receipt design. They demonstrate source-level ordering only, not a running adoption, scheduler or publication system.

## Adoption-fixed v1 path regression

These are separate symbolic variants. P1/E1 has validly adopted v1 with canonical path A = `planning/TRANSITION_ACTION.md`. B = `planning/actions/TRANSITION_ACTION.md` is a different proposed carrier path. The single journal path/blob/record binding validates the manifest in the exact successor carrier; duplicate files do not add another binding or migration semantics. All other authority, baseline, approval, fence, retention and eligibility checks still apply.

| Proposed transition / observation | Required result |
|---|---|
| P1 uses v1/A; candidate P2 stays on v1 but configures B | Reject before ref movement under P1's accepted v1 rules. Candidate approval/configuration cannot bridge the path change. P2 does not become accepted. |
| P2 configures B while the proposed event binds only A | Still reject before publication: satisfying the old location does not install an operative successor path. |
| P2 configures B with identical or different manifests at both A and B | Still reject. Two files, Git history or notification prose cannot replace a defined versioned migration contract or change the event's single-path meaning. |
| Unrelated P2 retains v1/A; its event binds A and the exact manifest there | May publish when all ordinary checks pass. After commit, eligibility and lost-wake replay resolve that same fixed A in E2's exact retained carrier. |
| P2 retains A but the proposed journal binding names B | Reject the mismatched binding before publication; a manifest copy at B does not satisfy the fixed A contract. If invalid suffix/evidence already exists, use existing recovery and fail-closed rules, never adopt it by convenience. |
| Recovery's actual invalid suffix mentions B, but last accepted P1 uses v1/A | Recovery candidate/event/manifest retain A from the accepted predecessor, not B from the unaccepted suffix. Ordinary recovery authority, retention and held-fence rules remain required. |
| Predecessor contract is `none`; P2 first adopts v1 with B | First-path establishment is permitted under predecessor-authorized adoption and complete baseline/fence rules. E2 binds B, which is then fixed for v1's lifetime; dispatch waits for valid adoption reconciliation and verified checks. No historical path/manifests are invented. |
| First root/child publication chooses v1 and an initial A or B | Bounded founding/parent authority approves that first path with the exact candidate/baseline. The adopting event/carrier binds it normally; first dispatch still waits for all adoption/eligibility checks. |

These cases define no path-migration adjunct or dual-path schema. A future move requires a separately specified versioned contract covering both boundaries, journal bindings, cold reconstruction, recovery and eligibility; current v1 rejects the move.
