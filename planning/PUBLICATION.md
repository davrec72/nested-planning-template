# Plan publication and root bootstrap

This file defines how a project discovers its **current accepted PlanRef**, how a new planning revision becomes operative, and how a root project creates its first authority state without inventing a pre-existing Role.

The publication protocol is separate from the Mermaid/node grammar. The current publication protocol is:

```text
plan-publication-v1
```

## Core distinction

Three facts must remain separate:

1. **repository content exists** — a commit containing proposed planning state exists;
2. **the planning state is approved** — valid authority has approved that exact commit;
3. **the planning state is current** — a valid publication record makes that exact commit the current accepted PlanRef.

A merge, branch head, file timestamp, or repository write does not by itself establish facts 2 or 3.

## Authoritative locator

Every instantiated project using this protocol MUST maintain:

```text
planning/CURRENT.md
```

on its configured authoritative/default branch.

That path is the authoritative **locator** for the current publication record. The mutable branch/path is not itself authority evidence. The record found there must be validated under this file.

The current accepted PlanRef is the exact `plan_ref` named by the latest valid publication record.

Agents MUST read planning files at that exact PlanRef when making authority, dispatch, acceptance, or dependency decisions. Do not substitute the default-branch head merely because it is newer.

The default branch MAY temporarily contain staged or merged planning content that has not yet been published. Such content is not operative until a valid publication record points to it.

## Publication record

`planning/CURRENT.md` must contain at least:

```text
publication_protocol: plan-publication-v1
publication_id: <stable unique ID>
plan_id: <PlanID>
grammar: <declared grammar of the accepted plan>
plan_ref: <exact commit SHA of the accepted planning state>
prior_plan_ref: <previous accepted PlanRef or none>
prior_publication_id: <previous publication ID or none>
prior_publication_commit: <commit carrying the previous CURRENT record or none>
approval_basis: role | founding | parent
approval_event: <durable locator proving approval of plan_ref>
approved_by_role: <RoleID or none>
approval_authority_source: <accepted source or none>
founding_record: <durable locator or none>
parent_authority_source: <durable locator or none>
publisher_identity: <attributable human/agent/process identity>
publication_authority_source: <source authorizing this publication action>
published_at: <timestamp or durable event time>
```

Fields that do not apply use `none`; do not omit them.

`plan_ref` is the accepted planning commit. It is deliberately **not** the later commit that writes or updates `planning/CURRENT.md`.

## Normal publication sequence

For an already initialized project, use this sequence.

### 1. Read the current publication

Resolve and validate `planning/CURRENT.md` from the authoritative branch.

Record:

```text
prior_publication_id
prior_publication_commit
prior_plan_ref
```

All authority for the proposed semantic change comes from the accepted state rooted at `prior_plan_ref` or another authority source already valid under that state.

### 2. Produce the candidate planning revision

Create/review the semantic planning or Role change normally.

The portable default is to merge/stage that semantic change first and identify the exact resulting commit:

```text
candidate_plan_ref=<exact commit SHA>
```

At this stage the candidate exists in repository history but is **not yet the current accepted PlanRef**.

Do not execute new authority or scheduling semantics merely because the candidate was merged/staged.

### 3. Approve the exact candidate

A Role with authority that existed before the change approves the exact `candidate_plan_ref` and produces a durable approval event.

Approval must identify at least:

```text
candidate_plan_ref
approving Role
approval authority source
semantic scope approved
```

If the candidate changes after approval, the approval does not silently follow it.

### 4. Publish the approval

Create a mechanical publication update to `planning/CURRENT.md` that points `plan_ref` to the exact approved candidate and chains to the prior publication.

Immediately before publication, verify that the authoritative `planning/CURRENT.md` still matches the recorded:

```text
prior_publication_id
prior_plan_ref
```

If either differs, the publication proposal is stale. Stop and reconcile against the newer current plan. Do not choose a winner from timestamps or merge order.

The publication update must not smuggle unreviewed semantic plan changes into the approved candidate. If semantic planning content changes after candidate approval, produce a new candidate and approval.

### 5. Publication becomes operative

Once the publication update itself is durably accepted/written under valid publication authority, the `plan_ref` named in that record becomes the current accepted PlanRef.

Foreman and other agents may then propagate/use the new state.

The publication carrier commit is evidence that the index changed; it does not replace `plan_ref`.

## Concurrent publications

Two proposals may be developed from the same prior PlanRef, but only a publication that correctly chains from the current valid publication may become current.

If proposal A publishes first, proposal B's previously recorded `prior_publication_id` / `prior_plan_ref` is stale. B must be reconciled against A and, where its validity depends on old planning state, re-reviewed/re-approved.

Do not resolve concurrent planning state by:

- latest timestamp;
- latest branch head;
- whichever notification arrived last;
- whichever agent has repository write access.

## Invalid or suspicious CURRENT records

Repository write access is not planning authority.

If the record at the authoritative locator is malformed, has a broken predecessor chain, names an unverifiable approval, or cites authority that did not exist at the prior accepted state:

1. do not use that record as current authority;
2. follow `prior_publication_commit` / file history to the most recent publication that can be validated;
3. stop affected new dispatch/decisions;
4. escalate the invalid publication for correction.

Do not silently repair authority history by editing old publication records in place.

## Root-project bootstrap

A root project has no parent plan and therefore cannot satisfy the ordinary rule "use a Role that already existed" before its first Role exists.

The template resolves this with one narrow exception: a **Founding Authority** external to the planning ontology may establish exactly the first accepted authority state.

The Founding Authority is not a Role and receives no continuing implicit project authority.

Before bootstrap, the project adopter must explicitly designate the Founding Authority and its trust basis. Repository ownership or write access alone is not enough.

Create `planning/FOUNDING.md` from `templates/FOUNDING.md` and include it in the first candidate planning commit.

A root founding record must identify:

```text
founding_record_id
project/repository identity
founding authority identity
external trust basis / evidence
bounded founding scope
initial Role/binding records being established
initial plan scope being ratified
```

### Root bootstrap sequence

1. An external project sponsor/owner/charter explicitly designates the Founding Authority and founding scope.
2. Prepare the first candidate commit containing the initial `PLAN`, `ROLES`, `FOUNDING`, grammar declaration, and other required planning files.
3. The Founding Authority approves that exact candidate commit through a durable founding approval event.
4. Create the first `planning/CURRENT.md` publication with:

```text
prior_plan_ref: none
prior_publication_id: none
prior_publication_commit: none
approval_basis: founding
founding_record: <locator to FOUNDING record in candidate_plan_ref>
```

5. Publish it under the founding authority described by the record.
6. The named `plan_ref` becomes the first current accepted PlanRef.
7. The founding exception expires.

After step 6, normal Role-based rules apply. Any continuing authority the founder should retain MUST be represented explicitly by a Role/binding established in the accepted planning state. Do not reuse `approval_basis: founding` for later ordinary changes.

The founding record is historical. After the first valid publication, do not rewrite the original founding act in place; record later amendments under ordinary accepted authority.

## Child-project bootstrap

A child repository does not need an independent root Founding Authority when an accepted parent contract/delegation already supplies its boundary authority.

Its first publication may use:

```text
approval_basis: parent
parent_authority_source: <accepted parent contract/delegation>
```

The exact parent authority must authorize the child scope and initial child authority state. After first publication, the child's internal Roles govern only within that delegated boundary.

Do not treat parent repository ownership or a similarly named Role as a delegation.

## Bootstrap limitation

Before the first valid publication, substantive project execution is not authorized by this protocol. Allowed pre-publication activity is limited to preparing, reviewing, and publishing the founding/parent-authorized initial state.

Foreman cannot be operationally bound before the state that creates its Role/binding becomes current.

## Publication versus milestone acceptance

Plan publication and Milestone acceptance are different protocols:

- Milestone acceptance decides whether a Milestone contract is satisfied.
- Plan publication decides which planning/authority snapshot is current.

A Milestone acceptance record cannot make an unpublished plan current. A plan publication cannot manufacture Milestone acceptance.

## What this protocol does not provide

This documentation does not provide cryptographic identity, signatures, or external identity verification. Projects needing stronger guarantees must add them.

The protocol does require explicit identity/evidence locators so a later reviewer can reconstruct what authority claim was relied upon instead of treating repository access as proof.