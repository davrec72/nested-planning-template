# Publication transition validation

This file is normative for `plan-publication-v1` and supplements `planning/PUBLICATION.md`.

## 1. Trust inputs

Git commit ancestry alone is not sufficient to prove which commit was historically the tip of a mutable ref. Every instantiated project therefore configures, during root/parent bootstrap, all of:

```text
publication_ref
publication_journal_kind
publication_journal_locator
publication_journal_trust_basis
plan_snapshot_retention_kind
plan_snapshot_retention_locator_or_pattern
plan_snapshot_retention_trust_basis
carrier_evidence_retention_kind
carrier_evidence_retention_locator_or_pattern
carrier_evidence_retention_trust_basis
```

The **publication journal** is a durable append-only or tamper-evident source, independent of the mutable publication ref, that a cold reader can access. Its trust contract must make deletion, reordering, or rewriting of committed publication events impossible under the configured trust model or detectably invalidate the journal.

Bare Git ancestry, a local reflog, or a mutable ref without such evidence is not a conforming publication journal.

The **carrier-evidence retention** contract is independently responsible for keeping every accepted publication carrier and the Git objects required to validate it cold-fetchable for at least the lifetime of the publication journal. A journal entry that merely names a carrier SHA is not enough.

If the configured journal, PlanRef retention, or carrier-evidence retention is unavailable, has a gap, or cannot establish the required historical evidence, ordinary substantive execution fails closed.

## 2. Accepted validator source

For an initialized project, the transition from accepted publication `Rn/Pn` to a successor is validated using the publication/governance rules contained in the **last accepted predecessor PlanRef `Pn`**.

A candidate may change `AGENTS.md`, `planning/PUBLICATION.md`, `planning/PUBLICATION_TRANSITIONS.md`, or related governance, but those changed rules do not validate the transition that makes the candidate current. Once validly published, they may govern the next transition.

For first root publication, the designated Founding Authority approves the exact first candidate plus the initial publication protocol/ref/journal/PlanRef-retention/carrier-retention contract. First child publication may analogously rely on accepted parent authority covering the same trust configuration.

## 3. Durable retention of semantic snapshots and carrier evidence

Before a publication event can commit, two distinct forms of evidence MUST be durably retained.

### 3.1 Published PlanRef retention

The exact candidate `plan_ref` MUST have a durable, cold-fetchable snapshot locator under the configured PlanRef-retention contract.

A conforming PlanRef snapshot mechanism must:

- retrieve the exact Git commit by SHA for a fresh reader;
- retain historical published PlanRefs for at least the lifetime of the publication journal;
- make deletion/repointing impossible under the configured trust model or detectably fail validation;
- remain independent of ordinary topic-branch cleanup, squash, or rebase.

Every publication journal event records:

```text
plan_ref
plan_snapshot_locator
plan_snapshot_retention_evidence
```

### 3.2 Publication-carrier evidence retention

The exact `successor_carrier_commit` MUST also have durable cold-fetchable evidence under the configured carrier-retention contract **before the journal event that accepts it commits**.

A conforming carrier-evidence mechanism must preserve enough exact Git evidence for a cold reader to perform every carrier check required by this protocol, including at least:

- the exact carrier commit object and SHA;
- its exact Git parent identity or identities;
- the carrier tree and exact `planning/CURRENT.md` content;
- any predecessor carrier objects needed to validate the event sequence;
- for a recovery transition, the quarantined invalid/uncommitted suffix from the divergence point through `invalid_suffix_tip`, or an authenticated retained representation sufficient to reproduce every protocol-required check on that suffix;
- the previously accepted carrier chain even when recovery proceeds on a divergent live branch and that accepted chain is no longer reachable from the new publication-ref tip.

Carrier evidence must remain cold-fetchable for at least the lifetime of the publication journal and must not depend on continued reachability from the mutable publication ref or ordinary repository branches.

Every accepted event records:

```text
successor_carrier_commit
carrier_evidence_locator
carrier_evidence_retention_evidence
```

A recovery event additionally records when applicable:

```text
accepted_predecessor_carrier_evidence_locator
invalid_suffix_evidence_locator
invalid_suffix_retention_evidence
```

The accepted predecessor locator may resolve through its earlier journal event; the recovery event must make that linkage explicit and verifiable.

If any historical PlanRef or carrier evidence required for validation is later missing or mismatched, cold reconstruction is not valid. Stop affected execution until conforming retained evidence is restored under already-valid authority; do not infer historical state from surviving text identifiers alone.

## 4. Publication journal event

Every accepted publication transition has exactly one committed journal event with at least:

```text
event_id
sequence
transition_kind: bootstrap | normal | recovery
plan_id
publication_protocol
publication_ref
ref_update_receipt
carrier_parent_commit
accepted_predecessor_commit
accepted_predecessor_event_id
successor_carrier_commit
carrier_evidence_locator
carrier_evidence_retention_evidence
accepted_predecessor_carrier_evidence_locator
publication_id
prior_publication_id
prior_plan_ref
plan_ref
plan_snapshot_locator
plan_snapshot_retention_evidence
invalid_suffix_start: none | <commit>
invalid_suffix_tip: none | <commit>
invalid_suffix_evidence_locator: none | <locator>
invalid_suffix_retention_evidence: none | <evidence>
approval_event
publication_authority_source
publisher_identity
committed_at
```

`ref_update_receipt` is durable evidence, under the configured journal/hosting trust contract, of the exact conditional ref movement attempted and its successful old/new object IDs. A self-authored statement in CURRENT is not sufficient.

The latest valid committed journal event is the publication high-water mark. The configured publication ref is an operational locator and MUST agree with that high-water mark except during a bounded uncommitted/invalid suffix that requires recovery.

An event is not valid merely because its named objects once existed. The journal event can commit only after both the PlanRef snapshot and all carrier evidence required by that event are durably retained under their configured contracts.

## 5. Normal publication transition

For `transition_kind=normal` after bootstrap:

```text
carrier_parent_commit == accepted_predecessor_commit
accepted_predecessor_commit == latest accepted successor_carrier_commit
prior_publication_id == predecessor publication_id
prior_plan_ref == predecessor plan_ref
```

The successor carrier's Git parent MUST equal the actual incumbent accepted carrier.

The publication ref update MUST be conditional/non-force from that exact carrier. A pre-write read is not serialization.

After the conditional update succeeds, retain the exact successor carrier evidence and verify its locator/evidence. The transition is not accepted until its journal event with the successful `ref_update_receipt`, retained PlanRef evidence, and retained carrier evidence is durably committed. If the ref moved but no valid journal event committed, the new carrier is an uncommitted suffix, not accepted state.

## 6. Recovery transition across an invalid suffix

A malformed, unauthorized, or uncommitted carrier may exist at the actual publication-ref tip without becoming accepted state.

Let:

```text
Rvalid = successor_carrier_commit of the latest valid journal event
X      = actual publication-ref tip
```

A bounded recovery may be performed under the governance and authority of `Rvalid`'s accepted PlanRef.

Create a recovery carrier `Y` with:

```text
transition_kind: recovery
carrier_parent_commit: X
accepted_predecessor_commit: Rvalid
accepted_predecessor_event_id: <latest valid event>
prior_publication_id: <from Rvalid>
prior_plan_ref: <from Rvalid>
invalid_suffix_start: <first commit after/divergent from Rvalid requiring quarantine>
invalid_suffix_tip: X
```

The Git parent of `Y` is the **actual tip X**, so the publication ref can advance non-force and the invalid suffix remains visible in the live Git ancestry. The accepted predecessor remains **Rvalid**; invalid carriers do not supply governance or authority.

Before the recovery journal event can commit, retain and verify:

1. the exact recovery carrier `Y` and its tree/CURRENT;
2. the entire quarantined invalid suffix needed for cold checks;
3. the previously accepted `Rvalid` carrier evidence through its earlier journal event, even if `Rvalid` is displaced from live-ref reachability;
4. the exact target PlanRef snapshot.

This rule is what makes divergent recovery cold-reconstructible after garbage collection: both the observed bad branch and the displaced accepted branch remain retrievable evidence even though the live graph may be `... -> X -> Y` and no longer reach `Rvalid`.

The recovery must have an explicit approval/authority source valid under `prior_plan_ref`. Its journal event records both the actual Git predecessor and the last accepted predecessor plus all required evidence locators.

Cold readers treat the invalid suffix as preserved but non-accepted history, then resume accepted publication history at the recovery event.

A recovery may republish the last accepted PlanRef or publish a newly approved candidate, provided its exact snapshot is retained and the approval is valid under the last accepted governance.

If the publication ref has been reset behind or moved to a divergent history, compare it to the journal high-water mark. If the accepted high-water carrier can be restored by a verified non-force ref movement, record that infrastructure repair in the journal without creating a new planning publication. Otherwise use an explicitly authorized recovery/migration that preserves the observed divergent tip and the last accepted predecessor as separate identities. Never infer that a reset consumed or restored founding authority.

## 7. Cold reconstruction

A cold reader starts from the configured publication journal, not from the mutable ref alone.

1. Resolve the trusted journal high-water event and verify event sequence/append-only integrity.
2. For every event, fetch the recorded retained `plan_ref` snapshot and verify the exact SHA.
3. For every event, fetch the retained carrier evidence and verify the exact carrier commit, tree, CURRENT content, and required parent relation.
4. Validate each transition under the accepted predecessor PlanRef's governance.
5. Verify each event's `ref_update_receipt`, carrier identities, publication fields, and evidence-retention records.
6. For normal transitions, require actual/accepted predecessor equality.
7. For recovery transitions, fetch and validate both the quarantined invalid suffix evidence and the separately retained last accepted predecessor carrier evidence.
8. Compare the live publication ref tip to the latest accepted journal event. A behind, divergent, or unjournaled-ahead tip is not silently accepted.

A ref reset from accepted R1 back to R0 is therefore detectable because the journal high-water still records R1 even though a fresh clone's Git ancestry at the current ref may resemble an older state. A later divergent recovery remains reconstructible because accepted R1 carrier evidence is retained independently of live-ref reachability.

## 8. Notification-to-transition binding

Notifications are wake/coordination messages, not authority.

Every published-change payload binds at least:

```text
publication_event_id
publication_id
publication_commit
new_plan_ref
prior_publication_id
prior_plan_ref
semantic_delta
active_work_impact
```

Before applying actions, Foreman verifies those identities against the validated journal and retained publication carrier evidence.

Foreman durably tracks the last applied publication event per relevant project/scope/package. Duplicate/already-applied notifications are idempotent. Stale notifications cannot reapply older pause/redirect actions after a newer event.

If notifications are skipped or arrive out of order, reconcile validated publication events from the last applied event through the journal high-water mark in order. After restart, recover last-applied state from durable coordination records; if unavailable, reconstruct conservatively before transition-specific actions.
