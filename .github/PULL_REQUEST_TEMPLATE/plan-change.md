## Semantic delta

Describe the planning meaning that changes. Do not merely describe the file diff.

## Current publication baseline

Resolve this from the valid `planning/CURRENT.md` before proposing the change:

```text
prior_publication_id:
prior_publication_commit:
prior_plan_ref:
```

Do not use the newest branch head as a substitute for `prior_plan_ref`.

## Affected milestones

- 

## Affected roles

- 

## Active work impact

Choose one per affected package/scope:

```text
none | continue | pause | redirect | supersede
```

## Authority impact

```text
none | binding change | scope change
```

If authority changes, cite the authority that existed before this PR and permits the change.

## Foreman dispatch required

```text
yes | no
```

Do not dispatch/propagate this candidate as current merely because the semantic PR merges. Foreman receives the operational delta only after the exact resulting candidate is approved and published through `planning/CURRENT.md` under `planning/PUBLICATION.md`.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

## Controlling decision / evidence

Link the accepted decision, delegation, or evidence that justifies the change.

## Post-merge/staging publication handoff

After the semantic change has a stable exact resulting commit, record:

```text
candidate_plan_ref:
approval_event:
approved_by_role:
approval_authority_source:
publication_required: yes
```

The candidate does not become current until a valid publication record points to that exact SHA.

If `planning/CURRENT.md` changes before publication, the publication proposal is stale and must be reconciled under `planning/PUBLICATION.md`.

## Validation checklist

- [ ] The baseline `prior_publication_id` / `prior_plan_ref` came from the valid current publication.
- [ ] This semantic candidate does not modify `planning/CURRENT.md`; publication is a separate step.
- [ ] The plan declares the intended grammar version, and any parent/child grammar compatibility or migration impact is explicit.
- [ ] Every node uses a defined class.
- [ ] Every solid dependency is a true hard prerequisite.
- [ ] Every dotted scheduling edge is labeled exactly `preferred before`.
- [ ] OR/N-of-M logic uses an explicit Gate.
- [ ] Every Decision has exactly one deciding Role.
- [ ] Every active Milestone has exactly one primary assigned Role.
- [ ] Every Milestone has exactly one status class.
- [ ] Every Milestone newly projected as `MILESTONE_DONE` indexes a valid prior acceptance receipt.
- [ ] Each receipt used for a DONE projection binds the exact pre-acceptance `contract_plan_ref`, accepted evidence, and independently valid acceptance authority for that milestone/scope.
- [ ] A materially changed milestone outcome, acceptance criteria, or authority contract does not silently inherit an older acceptance receipt.
- [ ] Issued acceptance receipts are preserved as immutable history; correction, revocation, or replacement is represented by later durable records rather than in-place rewriting.
- [ ] Non-DONE status changes cite the appropriate execution/pause/resume evidence and do not fabricate milestone acceptance.
- [ ] No proposed edit bootstraps its own authority, except the one-time root founding procedure explicitly allowed by `planning/PUBLICATION.md`.
- [ ] Child changes stay within the parent contract or parent authority is included.
- [ ] Active-work impact is explicit.
- [ ] Candidate approval will bind the exact resulting `candidate_plan_ref`.
- [ ] Foreman propagation is defined if needed, and occurs only after valid publication.
