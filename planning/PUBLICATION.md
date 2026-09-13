# Plan publication and root bootstrap

This file defines root bootstrap and how exact planning snapshots become current under `plan-publication-v1`.

`planning/PUBLICATION_TRANSITIONS.md` is normative for validator source, publication-journal evidence, recovery, retained snapshots, and notification matching.

## Core distinction

Keep these facts separate:

1. an exact candidate planning commit exists;
2. valid pre-existing authority approves that exact candidate;
3. the candidate has a durable retained snapshot;
4. the publication ref advances to a carrier naming the candidate;
5. a trusted publication-journal event commits evidence of that exact ref update;
6. only then is the candidate the current accepted PlanRef.

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
```

The publication journal must be durable and append-only/tamper-evident under its configured trust basis and readable by a cold successor. Bare Git ancestry or a local reflog alone is not sufficient evidence of historical ref movements.

The retention mechanism must keep every published exact PlanRef fetchable independently of ordinary work branches.

## Publication carrier

Each carrier on the configured publication ref contains `planning/CURRENT.md`.

A carrier records the accepted transition state, but the **trusted publication journal** establishes which ref updates actually became accepted transitions.

The latest valid committed journal event is the accepted publication high-water mark. The live publication ref must agree with that mark unless there is an invalid/uncommitted suffix being recovered.

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

Validate that the retained snapshot for `prior_plan_ref` is fetchable.

### 2. Prepare the semantic candidate

Create/review the plan or Role change and identify:

```text
candidate_plan_ref=<exact commit SHA>
```

The candidate is not current merely because it exists or merges.

### 3. Approve the exact candidate

The applicable authority approves that exact candidate under governance already valid before the change.

If candidate content changes, approval does not follow it.

### 4. Retain the candidate

Before publication, create/verify the configured durable snapshot for `candidate_plan_ref` and record its locator/evidence.

If the exact commit is not guaranteed cold-fetchable under the retention contract, publication must not proceed.

### 5. Prepare the successor carrier

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

### 6. Conditionally advance the publication ref

Advance the configured publication ref non-force from the exact actual incumbent carrier to the prepared successor carrier.

A stale sibling must fail rather than win by timestamp or merge order.

### 7. Commit the publication-journal event

After the successful conditional ref update, durably append the exact transition event and its `ref_update_receipt` to the configured trusted journal.

The transition becomes accepted only when that event is committed. If the ref moved but no journal event committed, the new carrier is an uncommitted suffix and ordinary execution remains governed by the latest valid journal event pending recovery.

### 8. Operate and propagate

Only after the journal event commits does the named `plan_ref` become current accepted planning state. Foreman may then apply the transition-bound semantic delta.

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

`Y` is a child of the actual tip so ref advancement remains non-force and the invalid suffix remains preserved. The invalid suffix is not treated as accepted governance or authority.

The recovery requires explicit authority valid under `prior_plan_ref`, a retained exact target PlanRef, a successful conditional ref update, and a committed recovery journal event recording both the actual Git predecessor and last accepted predecessor.

Cold reconstruction then treats the quarantined suffix as historical but non-accepted and resumes accepted publication history at the recovery event.

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
initial PlanRef retention kind/locator pattern
```

Bootstrap sequence:

1. designate the Founding Authority and bounded scope;
2. prepare the exact first candidate including required governance files;
3. Founding Authority approves the exact candidate plus initial publication/journal/retention contract;
4. retain the first candidate under the configured snapshot contract;
5. create the first carrier with `transition_kind: bootstrap` and no accepted predecessor;
6. establish the configured publication ref at that carrier;
7. commit the first trusted journal event, including the bootstrap ref-update/creation evidence;
8. the named `plan_ref` becomes the first current accepted PlanRef;
9. the founding exception expires.

Any continuing founder authority must appear as an ordinary Role/binding in the first accepted state.

## Child bootstrap

A child repository may bootstrap from accepted parent authority instead of an unrelated root founder. That parent authority must cover the child scope, initial Role state, initial publication protocol/ref, publication-journal trust contract, and snapshot-retention contract.

## Notification and Foreman recovery

Published-change messages are wake mechanisms, not authority. They must bind to the exact committed publication journal event and carrier. Stale/duplicate/out-of-order notifications are reconciled against journal order, not message arrival order.

If journal evidence, retained PlanRefs, or publication state is missing/contradictory, ordinary dependent execution fails closed.

## Security boundary

This template does not provide cryptographic identity/signature infrastructure. It does require an explicit trust basis for the publication journal and snapshot-retention mechanism so a cold reader knows what external durability assumptions it is relying on.
