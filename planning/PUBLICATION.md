# Plan publication and root bootstrap

This file defines root bootstrap and how exact planning snapshots become current under `plan-publication-v1`.

`planning/PUBLICATION_TRANSITIONS.md` is normative for validator source, publication-journal evidence, recovery, retained semantic snapshots, retained carrier evidence, and notification matching.

## Core distinction

Keep these facts separate:

1. an exact candidate planning commit exists;
2. valid pre-existing authority approves that exact candidate;
3. the candidate has a durable retained semantic snapshot;
4. the publication ref advances to a carrier naming the candidate;
5. the exact successor carrier and any required recovery suffix evidence are durably retained;
6. a trusted publication-journal event commits evidence of that exact ref update and those retained objects;
7. only then is the candidate the current accepted PlanRef.

A merge, branch head, timestamp, repository write, or message does not establish current planning state by itself.

## Bootstrap configuration

Every instantiated project fixes during root/parent bootstrap:

```text
publication_protocol: plan-publication-v1
publication_ref: refs/heads/plan-publications | <explicit alternative>
publication_journal_kind:
publication_journal_locator:
publication_journal_trust_basis:
plan_snapshot_retention_kind:
plan_snapshot_retention_locator_or_pattern:
plan_snapshot_retention_trust_basis:
carrier_evidence_retention_kind:
carrier_evidence_retention_locator_or_pattern:
carrier_evidence_retention_trust_basis:
transition_action_contract: none | transition-action-v1
transition_action_path: none | planning/TRANSITION_ACTION.md | <explicit carrier-tree path>
```

Predecessor-authorized `none` -> `transition-action-v1` adoption (including root/child bootstrap) chooses the first canonical path. Once accepted for this PlanID/publication configuration, that exact path is immutable for the lifetime of v1. Every later v1 normal/recovery candidate, journal path binding and successor carrier must use the predecessor accepted v1 path. Reject a proposed v1 path change before ref movement; duplicate files do not bridge paths. Future movement needs a separate explicit versioned migration contract, which v1 does not define. See `PUBLICATION_TRANSITIONS.md` section 9.

The publication journal must be durable and append-only/tamper-evident under its configured trust basis and readable by a cold successor. Bare Git ancestry or a local reflog alone is not sufficient evidence of historical ref movements.

The PlanRef-retention mechanism must keep every published exact PlanRef fetchable independently of ordinary work branches.

The carrier-evidence retention mechanism must keep every accepted publication carrier—and every Git object needed to perform the protocol's carrier checks—cold-fetchable independently of the mutable publication ref. For recovery, it must also retain the quarantined invalid/uncommitted suffix evidence required by the protocol. A carrier SHA written into a journal entry is not durable carrier evidence by itself.

## Operational execution eligibility

**Autonomous/Foreman-managed execution is eligible only while the current accepted publication configuration explicitly adopts `transition-action-v1`.** Its exact adoption-fixed carrier path must equal the journal path binding and resolve to the valid manifest, and its adoption/legacy baseline must be validly reconciled under `PUBLICATION_TRANSITIONS.md` section 9. Adoption is a prerequisite for this execution workflow, not an optional recovery enhancement.

`transition_action_contract: none` means **no autonomous Foreman dispatch**. It is permitted for planning-only/pre-execution configurations and systems with no dispatch capability. An inventory and read-only coordination may exist, but `none` never permits first or later dispatch/start/resume, or a new revision/attempt, rebind or supersession that creates execution obligations. An empty inventory, accepted Foreman binding or executor grant alone cannot enable that work.

A publication that remains in `none` mode may materially change planning only when no active/outstanding dispatch-capable execution obligation is affected and the accepted mode remains no-dispatch. Establish that impact under prior authority; do not equate missing inventory with no obligations. If legacy work is active/outstanding, block new dispatch/resume and any publication altering those obligations until prior-authorized reconciliation/migration establishes `transition-action-v1`, or the work is durably stopped/reconciled under valid legacy rules. The defined adopting transition is the migration path; a manifest-free material change cannot substitute for it or invent missing pause requests.

`transition-action-v1` is the only supported operational reconstruction contract. An unspecified "equivalent" does not qualify. A future alternative needs an explicitly versioned contract defining journal binding, completeness, fencing, replay, adoption/migration and failure semantics before compatibility can be claimed. Permitted representations or atomic fence implementations within v1 do not waive v1 adoption.

For first root/child publication intended to enable managed execution, adopt v1 and approve/publish its valid empty/baseline manifest in that first publication. Choosing `none` keeps bootstrap no-dispatch until later valid adoption. For every adoption, first block new obligation creation under predecessor governance, reconcile the complete legacy set through the predecessor high-water, and publish the conforming baseline manifest/fence under section 9. Enable dispatch only after the adopting event and all carried obligations are durably indexed/reconciled with required checks verified. Accepted publication alone does not settle that execution-enablement check; unresolved legacy or reconciliation failures fail closed.

## Publication carrier

Each carrier on the configured publication ref contains `planning/CURRENT.md`.

A carrier records the accepted transition state, but the **trusted publication journal** establishes which ref updates actually became accepted transitions.

The latest valid committed journal event is the accepted publication high-water mark. The live publication ref must agree with that mark unless there is an invalid/uncommitted suffix being recovered.

Every accepted carrier remains separately retrievable through the carrier-evidence retention contract for at least the lifetime of the publication journal, even if later divergent recovery makes it unreachable from the live publication-ref tip.

After explicit `transition-action-v1` adoption, every planning carrier also contains its immutable transition-action manifest at the fixed accepted path, including a checked no-impact manifest. The existing journal binds that same path/blob/record ID in the exact successor carrier; existing carrier retention preserves it and its reconstruction inputs. This is not a second journal or new currentness protocol. Adoption/legacy rules and exact schema validation are in `PUBLICATION_TRANSITIONS.md` section 9 and `templates/TRANSITION_ACTION.md`.

## CURRENT fields

Every carrier records at least:

```text
publication_protocol: plan-publication-v1
transition_kind: bootstrap | normal | recovery
publication_id
plan_id
grammar
plan_ref
plan_snapshot_locator
plan_snapshot_retention_evidence
carrier_parent_commit
accepted_predecessor_commit
accepted_predecessor_event_id
prior_publication_id
prior_plan_ref
invalid_suffix_start: none | <commit>
invalid_suffix_tip: none | <commit>
approval_basis: role | founding | parent
approval_event
approved_by_role
approval_authority_source
founding_record
parent_authority_source
publisher_identity
publication_authority_source
publication_journal_event_id
published_at
```

Fields that do not apply use `none`.

`plan_ref` is the accepted semantic planning snapshot. The carrier commit is publication-history evidence and is not itself automatically the PlanRef.

Carrier retention locators/evidence live in the trusted journal event rather than needing to self-reference from `CURRENT`, because the exact carrier SHA is not known until the carrier commit exists.

## Which rules validate a transition

For every publication after bootstrap, the **last accepted predecessor PlanRef's governance** validates the next transition.

A candidate may change publication/governance rules, but those new rules cannot validate the transition that makes themselves current. Once accepted, they may govern a later transition.

## Normal publication sequence

### 1. Resolve accepted state

Read the configured trusted publication journal and validate its high-water event under `planning/PUBLICATION_TRANSITIONS.md`.

Record:

```text
accepted_predecessor_event_id
accepted_predecessor_commit
prior_publication_id
prior_plan_ref
```

Validate that both the retained semantic snapshot for `prior_plan_ref` and the retained carrier evidence for `accepted_predecessor_commit` are cold-fetchable.

When `transition-action-v1` applies, also resolve the serialized execution inventory and retain the exact impact-analysis baseline/obligation set. Prepare the preallocated fence ID and exact scope/domain for approval. Later conditional acquisition must match that baseline and exclude affected obligation-creating mutations through valid journal commit; a reread is insufficient. Changed baseline requires rebuilding/reapproving the manifest and carrier under section 9.

### 2. Prepare the semantic candidate

Create/review the plan or Role change and identify:

```text
candidate_plan_ref=<exact commit SHA>
```

The candidate is not current merely because it exists or merges.

For `transition-action-v1`, now prepare the exact carrier-resident manifest binding this candidate, preallocated event/publication/fence IDs, exact inventory baseline/obligation set, fence scope/domain and explicit affected-attempt obligations (or checked empty impact). Preallocate an approval-event ID if needed; the manifest contains neither its own blob hash nor its future carrier SHA. Fence scope covers potential affected attempts as well as those already listed.

### 3. Approve the exact candidate

The applicable authority approves that exact candidate under governance already valid before the change.

If candidate content changes, approval does not follow it.

An applicable transition-action manifest also needs predecessor-valid approval explicitly binding its final blob identity and record ID. The same candidate approval may cover it only when it binds both exact objects; otherwise obtain a separate manifest approval. Changed manifest content requires new approval.

### 4. Retain the semantic candidate

Before publication, create/verify the configured durable snapshot for `candidate_plan_ref` and record its locator/evidence.

If the exact commit is not guaranteed cold-fetchable under the PlanRef-retention contract, publication must not proceed.

### 5. Prepare and move to the successor carrier

For a normal transition:

```text
transition_kind: normal
carrier_parent_commit == accepted_predecessor_commit
accepted_predecessor_commit == latest accepted journal carrier
accepted_predecessor_event_id == latest accepted journal event
prior_publication_id == predecessor publication_id
prior_plan_ref == predecessor plan_ref
invalid_suffix_start: none
invalid_suffix_tip: none
```

Prepare the exact successor carrier and advance the configured publication ref non-force/conditionally from the exact actual incumbent accepted carrier to that successor carrier.

For `transition-action-v1`, the carrier contains CURRENT plus the exact approved manifest and reconstruction inputs. After approval and before ref movement, conditionally acquire the preallocated durable publication/dispatch fence against the exact analyzed baseline in the same mechanism as inventory/dispatch claims. A changed baseline requires rebuild/reapproval. Hold through valid trusted journal commit; every affected obligation-creating/broadening dispatch/start/resume/rebinding/revision/attempt mutation checks the current fence through the same serialization and blocks while held. A plain reread is insufficient. Follow `PUBLICATION_TRANSITIONS.md` section 9 for scope, permitted observations and durable proof.

A stale sibling must fail rather than win by timestamp or merge order.

### 6. Retain the exact carrier evidence

After the successful ref update and before acceptance, retain the exact successor carrier under the bootstrap-fixed carrier-evidence contract. Verify that a cold reader can retrieve the exact carrier commit, tree, `planning/CURRENT.md`, and required parent evidence.

For an applicable manifest, this includes its journal-bound path/blob content and the exact inventory/analysis inputs needed to reconstruct the actions. A retained CURRENT alone is insufficient.

If the carrier evidence cannot be durably retained, do not commit the publication journal event. The advanced ref remains an uncommitted suffix governed by the previous accepted journal high-water pending recovery.

### 7. Commit the publication-journal event

Durably append the exact transition event to the configured trusted journal, including:

- the successful `ref_update_receipt`;
- PlanRef snapshot locator/evidence;
- carrier evidence locator/evidence;
- accepted predecessor identities and evidence linkage.
- when `transition-action-v1` applies, the exact manifest contract/path/blob/record ID, analyzed baseline and fence ID/scope/acquisition/held-through-commit evidence required by `PUBLICATION_TRANSITIONS.md`.

The transition becomes accepted only when that event is committed. If the ref moved but no conforming journal event committed, the new carrier is an uncommitted suffix and ordinary execution remains governed by the latest valid journal event pending recovery.

### 8. Operate and propagate

Only after the journal event commits does the named `plan_ref` become current accepted planning state. Foreman may then apply the transition-bound semantic delta.

For `transition-action-v1`, Foreman reconstructs all missing request/receipt/check obligations from the exact retained manifest even if the initial wake is lost, and only then advances its publication-reconciliation marker. A valid explicit empty manifest creates no receipts; an affected `continue` is not empty.

Normal fence release occurs durably only after the valid journal commit; subsequent dispatch validates newly accepted state and outstanding transition obligations. If release fails, keep execution conservatively blocked until a successor verifies that exact event and releases it. The existing journal is still the sole accepted-publication/currentness boundary.

## Recovery from an invalid or uncommitted tip

Do not rewrite or reset publication history to hide a bad tip.

Let:

```text
Rvalid = successor carrier in latest valid journal event
X      = actual publication-ref tip
```

A recovery transition is validated under `Rvalid`'s accepted PlanRef and may create `Y` with:

```text
transition_kind: recovery
carrier_parent_commit: X
accepted_predecessor_commit: Rvalid
accepted_predecessor_event_id: <latest valid journal event>
prior_publication_id: <from Rvalid>
prior_plan_ref: <from Rvalid>
invalid_suffix_start: <first quarantined commit>
invalid_suffix_tip: X
```

`Y` is a child of the actual tip so ref advancement remains non-force and the invalid suffix remains visible in live Git ancestry. The invalid suffix is not treated as accepted governance or authority.

Before the recovery journal event may commit, retain/verify all of:

1. the exact target PlanRef snapshot;
2. the exact recovery carrier `Y`, including tree/CURRENT and parent evidence;
3. the quarantined invalid suffix from the divergence point through `X`, or authenticated retained evidence sufficient to perform every required suffix check;
4. the displaced accepted carrier `Rvalid` and the earlier accepted carrier chain needed for cold validation, through their previously committed carrier-evidence locators.

Thus divergent recovery may move the live graph onto `... -> X -> Y` without losing the separately retained accepted `Rvalid` branch. Garbage collection or live-ref rewrites cannot silently erase the accepted carrier evidence that the trusted journal still requires.

The recovery requires explicit authority valid under `prior_plan_ref`, a successful conditional ref update, and a committed recovery journal event recording the actual Git predecessor, the last accepted predecessor, and all required retained evidence locators.

Cold reconstruction treats the quarantined suffix as historical but non-accepted and resumes accepted publication history at the recovery event.

An adopted recovery publication also carries its own approved transition-action manifest under the last accepted predecessor authority, even if it republishes the same PlanRef. Preserve earlier accepted manifests with their retained carriers. A manifest in an uncommitted suffix is not accepted action authority; carrier/manifest-retention or journal failure follows the same recovery rules above.

Publication fences survive these failures. Before-ref failure permits release only after verified durable abort. After ref movement, keep the fence held through explicitly authorized recovery, or durably abort/reconcile/classify the uncommitted suffix before releasing to predecessor-governed execution. Any later publication after release requires a fresh baseline/manifest/approval/fence. Crash/succession discovers active fences in durable inventory; timeout/lease expiry is not a safe release. Section 9 defines the required proof and continuous coverage during recovery.

If the live ref is merely behind the journal high-water mark and can be restored by a verified non-force movement to the already-accepted carrier, record that infrastructure repair in the journal; do not create a fictional new planning acceptance.

## Root-project bootstrap

A root project has no prior Role. One narrow external **Founding Authority** may establish the first accepted plan/Role/governance state.

Repository ownership or write access alone is not the Founding Authority.

The founding record must identify:

```text
founding authority identity and trust basis
bounded founding scope
initial plan/Role state
initial publication protocol/ref
initial publication journal kind/locator/trust basis
initial PlanRef retention kind/locator pattern/trust basis
initial carrier-evidence retention kind/locator pattern/trust basis
```

Bootstrap sequence:

1. designate the Founding Authority and bounded scope;
2. prepare the exact first candidate including required governance files;
3. Founding Authority approves the exact candidate plus initial publication/journal/PlanRef-retention/carrier-retention contract;
4. retain the first candidate under the configured semantic snapshot contract;
5. create the first carrier with `transition_kind: bootstrap` and no accepted predecessor;
6. establish the configured publication ref at that carrier;
7. retain the exact first carrier evidence under the configured carrier contract;
8. commit the first trusted journal event, including bootstrap ref-update/creation evidence and both retention receipts;
9. the named `plan_ref` becomes the first current accepted PlanRef;
10. the founding exception expires.

Any continuing founder authority must appear as an ordinary Role/binding in the first accepted state.

When adopting `transition-action-v1` at bootstrap, prepare the empty/baseline manifest after the exact first candidate and before approval. Founding Authority approves both exact objects and configuration; include the manifest in the first carrier, retain it with that carrier, and bind it in the first journal event. Predecessor/legacy fields are `none`. Do not infer no active execution without an explicit basis.

Only a first root/child publication with no pre-existing dispatch-capable execution system may omit the inventory fence with that explicit basis. An adopted inventory requires fencing even for no-impact publication. Legacy active/still-dispatchable execution requires predecessor-valid exclusion: stop/reconcile it and exclude further dispatch, or establish a bounded one-time fence under prior authority. Candidate rules cannot authorize their own adoption fence; follow section 9 rather than fabricating historical fences.

## Child bootstrap

A child repository may bootstrap from accepted parent authority instead of an unrelated root founder. That parent authority must cover the child scope, initial Role state, initial publication protocol/ref, publication-journal trust contract, PlanRef-retention contract, and carrier-evidence retention contract.

It may likewise authorize initial `transition-action-v1` adoption and the exact child baseline manifest within that bounded bootstrap. Existing projects instead follow the predecessor-approved adoption/legacy reconciliation in `PUBLICATION_TRANSITIONS.md` section 9; historical events are neither invalidated nor given invented manifests.

## Notification and Foreman recovery

Published-change messages are wake mechanisms, not authority. They must bind to the exact committed publication journal event and carrier. Stale/duplicate/out-of-order notifications are reconciled against journal order, not message arrival order.

If journal evidence, retained PlanRefs, retained carrier evidence, or publication state is missing/contradictory, ordinary dependent execution fails closed.

## Security boundary

This template does not provide cryptographic identity/signature infrastructure. It does require explicit trust bases for the publication journal, PlanRef retention, and carrier-evidence retention so a cold reader knows what external durability assumptions it is relying on.
