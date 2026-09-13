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
```

The **publication journal** is a durable append-only or tamper-evident source, independent of the mutable publication ref, that a cold reader can access. Its trust contract must make deletion, reordering, or rewriting of committed publication events impossible under the configured trust model or detectably invalidate the journal.

Bare Git ancestry, a local reflog, or a mutable ref without such evidence is not a conforming publication journal.

If the configured journal is unavailable, has a gap, or cannot establish its high-water event, ordinary substantive execution fails closed.

## 2. Accepted validator source

For an initialized project, the transition from accepted publication `Rn/Pn` to a successor is validated using the publication/governance rules contained in the **last accepted predecessor PlanRef `Pn`**.

A candidate may change `AGENTS.md`, `planning/PUBLICATION.md`, `planning/PUBLICATION_TRANSITIONS.md`, or related governance, but those changed rules do not validate the transition that makes the candidate current. Once validly published, they may govern the next transition.

For first root publication, the designated Founding Authority approves the exact first candidate plus the initial publication protocol/ref/journal/retention contract. First child publication may analogously rely on accepted parent authority.

## 3. Durable retention of published PlanRefs

Before a publication can commit, the exact candidate `plan_ref` MUST have a durable, cold-fetchable snapshot locator under the configured retention contract.

A conforming snapshot mechanism must:

- retrieve the exact Git commit by SHA for a fresh reader;
- retain historical published PlanRefs for at least the lifetime of the publication journal;
- make deletion/repointing impossible under the configured trust model or detectably fail validation;
- remain independent of ordinary topic-branch cleanup, squash, or rebase.

Examples may include a protected immutable snapshot ref or a permanent object/archive service, but the template does not prescribe a provider.

Every publication journal event records:

```text
plan_ref
plan_snapshot_locator
plan_snapshot_retention_evidence
```

If a required historical snapshot is later missing or mismatched, cold reconstruction is not valid; stop affected execution and recover the retained snapshot before proceeding.

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
publication_id
prior_publication_id
prior_plan_ref
plan_ref
plan_snapshot_locator
plan_snapshot_retention_evidence
invalid_suffix_start: none | <commit>
invalid_suffix_tip: none | <commit>
approval_event
publication_authority_source
publisher_identity
committed_at
```

`ref_update_receipt` is durable evidence, under the configured journal/hosting trust contract, of the exact conditional ref movement attempted and its successful old/new object IDs. A self-authored statement in CURRENT is not sufficient.

The latest valid committed journal event is the publication high-water mark. The configured publication ref is an operational locator and MUST agree with that high-water mark except during a bounded uncommitted/invalid suffix that requires recovery.

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

After the conditional update succeeds, the transition is not accepted until its journal event with the successful `ref_update_receipt` is durably committed. If the ref moved but no journal event committed, the new carrier is an uncommitted suffix, not accepted state.

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

The Git parent of `Y` is the **actual tip X**, so the publication ref can advance non-force and the invalid suffix remains preserved in history. The accepted predecessor remains **Rvalid**; invalid carriers do not supply governance or authority.

The recovery must have an explicit approval/authority source valid under `prior_plan_ref`. Its journal event records both the actual Git predecessor and the last accepted predecessor.

Cold readers treat the invalid suffix as preserved but non-accepted history, then resume accepted publication history at the recovery event.

A recovery may republish the last accepted PlanRef or publish a newly approved candidate, provided its exact snapshot is retained and the approval is valid under the last accepted governance.

If the publication ref has been reset behind or moved to a divergent history, compare it to the journal high-water mark. If the accepted high-water carrier can be restored by a verified non-force ref movement, record that infrastructure repair in the journal without creating a new planning publication. Otherwise use an explicitly authorized recovery/migration that preserves the observed divergent tip and the last accepted predecessor as separate identities. Never infer that a reset consumed or restored founding authority.

## 7. Cold reconstruction

A cold reader starts from the configured publication journal, not from the mutable ref alone.

1. Resolve the trusted journal high-water event and verify event sequence/append-only integrity.
2. For every event, fetch the recorded retained `plan_ref` snapshot and verify the exact SHA.
3. Validate each transition under the accepted predecessor PlanRef's governance.
4. Verify each event's `ref_update_receipt`, carrier identities, and publication fields.
5. For normal transitions, require actual/accepted predecessor equality.
6. For recovery transitions, validate the quarantined invalid suffix and the separate last accepted predecessor exactly as specified above.
7. Compare the live publication ref tip to the latest accepted journal event. A behind, divergent, or unjournaled-ahead tip is not silently accepted.

A ref reset from accepted R1 back to R0 is therefore detectable because the journal high-water still records R1 even though a fresh clone's Git ancestry at the current ref may resemble an older state.

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

Before applying actions, Foreman verifies those identities against the validated journal and publication carrier.

Foreman durably tracks the last applied publication event per relevant project/scope/package. Duplicate/already-applied notifications are idempotent. Stale notifications cannot reapply older pause/redirect actions after a newer event.

If notifications are skipped or arrive out of order, reconcile validated publication events from the last applied event through the journal high-water mark in order. After restart, recover last-applied state from durable coordination records; if unavailable, reconstruct conservatively before transition-specific actions.
