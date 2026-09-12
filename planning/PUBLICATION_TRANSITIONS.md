# Publication transition validation

This file is normative for `plan-publication-v1` and supplements `planning/PUBLICATION.md`. Where the earlier prose is less specific, this file controls transition validation, discovery, and notification matching.

## 1. Accepted validator source

Do not use unpublished governance text from the default branch to discover accepted state.

For an initialized project, the transition from accepted publication `Rn/Pn` to `Rn+1/Pn+1` is validated using the publication/governance rules contained in the predecessor accepted PlanRef `Pn`.

A candidate may change `planning/PUBLICATION.md`, `AGENTS.md`, or related governance files, but those changed rules do not govern the transition that makes the candidate current. Once the candidate is validly published, its accepted rules may govern the next transition.

Rule:

```text
predecessor accepted rules validate the transition to successor accepted rules
```

For the first root publication there is no predecessor PlanRef. The designated Founding Authority must approve both the exact first candidate and the initial publication protocol used to create its first carrier. A child bootstrap may analogously rely on accepted parent authority.

## 2. Dedicated serialized publication ref

Each instantiated project configures one publication ref. Portable default:

```text
refs/heads/plan-publications
```

Its tip is the authoritative publication carrier. Each carrier contains `planning/CURRENT.md`.

The publication ref MUST advance only by a non-force fast-forward from the exact incumbent carrier. A reset, force update, replay to an ancestor, or carrier whose Git parent is not the incumbent carrier is not a valid publication transition.

Semantic plan/Role candidates may live on normal branches and may even be merged there before publication; those branches are not the publication history.

## 3. Publication carrier invariants

For every publication after the first, CURRENT must name:

```text
prior_publication_commit=<exact incumbent carrier commit>
prior_publication_id=<ID in incumbent CURRENT>
prior_plan_ref=<PlanRef in incumbent CURRENT>
```

The new carrier's Git parent MUST equal `prior_publication_commit`.

The publication-ref update MUST conditionally advance from that exact predecessor carrier. A pre-write read is not enough serialization. If another publisher advances first, the stale update must fail or be rejected and reconciled.

## 4. Cold reconstruction

A cold reader determines current state from the configured publication-ref history, not from CURRENT's self-reported predecessor fields alone.

Validate the carrier chain from the first accepted publication to the ref tip. For each transition:

1. carrier Git parent equals CURRENT.prior_publication_commit;
2. CURRENT.prior_publication_id and prior_plan_ref equal the validated predecessor record;
3. the transition is valid under the predecessor PlanRef's accepted governance rules;
4. the exact candidate approval and publication authority are valid;
5. the carrier is part of the non-force descendant history of the configured publication ref.

A record that skips an incumbent, restores an old CURRENT payload at a later carrier, or appears only through rewritten publication-ref history is not accepted merely because its internal predecessor fields look coherent.

If the ref tip is invalid, inspect the authoritative carrier history and recover the most recent valid predecessor transition. Do not rely on the suspect record's own pointer as the sole recovery route.

### Concurrency example

From `R0/P0`, A and B may both prepare publications. If A successfully advances `R0 -> R1`, B's attempted `R0 -> R2` is stale. B must reconcile on R1; it cannot become current by timestamp or by writing a CURRENT record that still claims R0.

### Replay example

After `R0 -> R1`, writing the old R0 CURRENT payload into a new commit does not restore R0. Reversion requires a new authorized transition whose predecessor is the actual incumbent R1 carrier.

## 5. Notification-to-transition binding

Notifications are wake/coordination messages, not state authority.

Every published-change payload must bind to one accepted publication transition:

```text
publication_id
publication_commit
new_plan_ref
prior_publication_id
prior_plan_ref
semantic_delta
active_work_impact
```

Before applying actions, Foreman must verify those identities against the validated publication history.

Foreman must durably track the last applied publication per relevant project/scope/package. Duplicate or already-applied notifications are idempotent. A stale notification must not reapply an older pause/redirect after a newer publication superseded it.

If notifications were missed or arrive out of order, reconcile all validated publication transitions from the last applied publication through CURRENT in order. After restart, recover last-applied state from durable coordination records; if unavailable, reconstruct conservatively before taking transition-specific actions.

Reading CURRENT alone is not enough to justify applying an arbitrary notification's action payload.
