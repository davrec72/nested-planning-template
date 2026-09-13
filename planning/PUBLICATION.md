# Plan publication and root bootstrap

This file defines how a project discovers its **current accepted PlanRef**, how a new planning revision becomes operative, and how a root project creates its first authority state without inventing a pre-existing Role.

The publication protocol is separate from the plan grammar. The current publication protocol is:

```text
plan-publication-v1
```

`planning/PUBLICATION_TRANSITIONS.md` is normative for validator source, serialized carrier history, cold reconstruction, recovery, and notification matching. Where older prose is less specific, that file controls.

## Core distinction

Keep four facts separate:

1. **candidate content exists** — an exact commit contains proposed planning state;
2. **candidate content is approved** — valid pre-existing authority approves that exact commit;
3. **the approval is published** — the authoritative publication ref advances to a valid carrier naming that exact candidate;
4. **the planning state is current** — the candidate named by the validated publication-ref tip is the current accepted PlanRef.

A merge, default-branch head, timestamp, notification, or repository write does not by itself establish facts 2–4.

## Authoritative publication history

`plan-publication-v1` uses one serialized publication ref:

```text
refs/heads/plan-publications
```

An instantiated project may choose a different ref only if that exact locator is fixed by its founding/parent bootstrap record before the first publication. Changing the publication ref later requires an explicit protocol migration under already-current authority; do not silently switch locators.

Each publication carrier on that ref contains:

```text
planning/CURRENT.md
```

The **publication-ref tip**, after validation of its carrier history, is the authoritative locator for current accepted planning state.

The semantic/default branch may contain newer staged or merged planning content. Such content is not operative until a valid publication carrier names it.

## Which rules validate publication

Do not use unpublished governance text to decide whether incumbent accepted state is valid.

For every transition after the first:

```text
predecessor accepted PlanRef governance
    validates
successor publication transition
```

If candidate `Pn+1` changes `AGENTS.md`, `planning/PUBLICATION.md`, `planning/PUBLICATION_TRANSITIONS.md`, or related governance, those changed rules do **not** validate the transition that makes `Pn+1` current. After `Pn+1` is validly published, its rules may govern the next transition.

The first root publication has no predecessor. Its Founding Authority must explicitly approve both the exact first candidate and the exact initial publication protocol/locator being used. A first child publication may instead derive that bootstrap authority from an accepted parent contract/delegation.

## Publication record

Every carrier's `planning/CURRENT.md` identifies at least:

```text
publication_protocol: plan-publication-v1
publication_id: <stable unique ID>
plan_id: <PlanID>
grammar: <grammar declared by plan_ref>
plan_ref: <exact accepted planning commit SHA>
prior_plan_ref: <previous accepted PlanRef or none>
prior_publication_id: <previous publication ID or none>
prior_publication_commit: <exact predecessor publication carrier or none>
approval_basis: role | founding | parent
approval_event: <durable locator proving approval of plan_ref>
approved_by_role: <RoleID or none>
approval_authority_source: <accepted source or none>
founding_record: <durable locator or none>
parent_authority_source: <durable locator or none>
publisher_identity: <attributable identity>
publication_authority_source: <source authorizing publication>
published_at: <timestamp or durable event time>
```

Fields that do not apply use `none`.

`plan_ref` is the accepted planning snapshot. The carrier commit is publication-history evidence and is not automatically the PlanRef.

## Normal publication sequence

### 1. Resolve current state

Read and validate the configured publication-ref history under `planning/PUBLICATION_TRANSITIONS.md`.

Record from the validated tip:

```text
prior_publication_commit
prior_publication_id
prior_plan_ref
```

All ordinary approval/publication authority for the proposed change must already be valid under `prior_plan_ref` or another authority source already valid there.

### 2. Produce the candidate

Prepare/review the semantic planning or Role change normally and identify the exact resulting commit:

```text
candidate_plan_ref=<exact commit SHA>
```

The candidate may live on or be merged into a normal branch. It is not current merely because it exists.

A semantic candidate must not rely on editing publication history in place.

### 3. Approve the exact candidate

The applicable Role approves the exact `candidate_plan_ref` and records at least:

```text
candidate_plan_ref
approving Role
approval authority source
semantic scope approved
```

If candidate content changes, the old approval does not follow it.

### 4. Prepare the successor carrier

Create a carrier whose `planning/CURRENT.md` points to `candidate_plan_ref` and names the exact validated predecessor values.

For every publication after the first:

```text
carrier Git parent == prior_publication_commit
CURRENT.prior_publication_commit == prior_publication_commit
CURRENT.prior_publication_id == predecessor CURRENT.publication_id
CURRENT.prior_plan_ref == predecessor CURRENT.plan_ref
```

Validate the transition using the predecessor accepted PlanRef's publication/governance rules.

### 5. Serialize the publication

Advance the configured publication ref **non-force** from the exact incumbent carrier to the prepared successor carrier.

A pre-write read is not sufficient serialization. The ref update itself must fail/reject if another publisher advanced first.

If another publication wins first, reconcile the candidate against the new current state and determine whether renewed review/approval is required.

### 6. Publication becomes operative

Once the successor carrier is the validated publication-ref tip, the `plan_ref` named there is current accepted planning state.

Only then may Foreman or other agents propagate and act on transition-specific planning changes.

## Concurrency, replay, and recovery

Two publishers may prepare from the same predecessor, but only one can advance the publication ref from that exact carrier. A stale sibling carrier cannot become current by timestamp, merge order, notification order, or a self-reported predecessor field.

Replaying old `CURRENT` contents after a later publication does not restore old state. Reversion requires a new authorized successor carrier whose predecessor is the actual incumbent carrier.

If the publication-ref tip is malformed or unauthorized:

1. do not use it as current authority;
2. inspect the actual carrier ancestry on the publication ref;
3. validate transitions in order under predecessor accepted governance;
4. recover the most recent valid predecessor carrier;
5. stop affected new dispatch/decisions until the invalid tip is corrected under valid authority.

Do not use a suspect record's own predecessor pointer as the sole recovery route and do not rewrite old carrier history in place.

## Notification and propagation

Notifications are wake/coordination messages, not authority.

Every published-change payload must bind to one publication transition:

```text
publication_id
publication_commit
new_plan_ref
prior_publication_id
prior_plan_ref
semantic_delta
active_work_impact
```

Before applying actions, Foreman validates those identities against publication history and compares them to durable last-applied publication state for the relevant scope/package.

Duplicate notifications are idempotent. Stale notifications must not reapply superseded pause/redirect instructions. If notifications are missed or arrive out of order, reconcile validated transitions from the last applied publication through current state in order.

See `planning/PUBLICATION_TRANSITIONS.md` for the normative procedure.

## Root-project bootstrap

A root project has no prior Role. The template therefore permits one narrow external exception: a **Founding Authority** external to the Role ontology may establish exactly the first accepted authority state.

Repository ownership/write access alone is not the Founding Authority.

Create `planning/FOUNDING.md` from `templates/FOUNDING.md`. The record must identify:

```text
founding_record_id
project/repository identity
founding authority identity
external trust basis/evidence
bounded founding scope
initial plan scope
initial Role/binding records
initial publication protocol/locator
```

Bootstrap sequence:

1. external sponsor/owner/charter explicitly designates the Founding Authority and bounded founding scope;
2. prepare the exact first candidate containing PLAN, ROLES, FOUNDING, grammar, and required governance files;
3. Founding Authority approves that exact candidate and the exact initial publication protocol/locator;
4. create the first publication carrier with `prior_*: none` and `approval_basis: founding`;
5. establish the configured publication ref at that carrier;
6. validate the first carrier under the approved founding protocol;
7. the named `plan_ref` becomes the first current accepted PlanRef;
8. the founding exception expires.

Any continuing founder authority must appear as an ordinary Role/binding in the first accepted state. Do not reuse founding authority for later ordinary changes.

## Child-project bootstrap

A child repository need not create an unrelated root Founding Authority when an accepted parent contract/delegation supplies its boundary authority.

Its first publication may use:

```text
approval_basis: parent
parent_authority_source: <accepted parent contract/delegation>
```

The parent source must authorize the child scope, initial authority state, and initial publication protocol/locator. After bootstrap, child Roles govern only within the delegated boundary.

## Bootstrap limitation

Before the first valid publication, substantive project execution is not initialized by this protocol. Permitted pre-publication activity is limited to preparing, reviewing, approving, and publishing the founding/parent-authorized initial state.

Foreman cannot be operationally bound before the state creating that Role/binding is current.

## Publication versus Milestone acceptance

These are separate protocols:

- Milestone acceptance decides whether a Milestone contract is satisfied.
- Plan publication decides which planning/authority snapshot is current.

Neither protocol manufactures the other.

## Security boundary

This documentation does not provide cryptographic identity/signatures or external identity verification. Projects needing those guarantees must add them.

It does require attributable identities and durable evidence locators so later reviewers can reconstruct the authority claim actually relied upon.