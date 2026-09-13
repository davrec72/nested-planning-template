## Semantic delta

Describe the planning meaning that changes. Do not merely describe the file diff.

## Current publication baseline

Resolve from validated publication-ref history:

```text
publication_ref:
prior_publication_commit:
prior_publication_id:
prior_plan_ref:
```

Do not use newest default-branch content as accepted state or use candidate governance to validate its own transition.

## Affected milestones

- 

## Affected roles

- 

## Active work impact

```text
none | continue | pause | redirect | supersede
```

## Authority impact

```text
none | binding change | scope change
```

If authority changes, cite authority valid before this candidate.

## Foreman dispatch required

```text
yes | no
```

Do not propagate the candidate merely because it merges. Propagation begins only after a valid successor publication carrier becomes the publication-ref tip.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

## Controlling decision / evidence

Link the accepted decision, delegation, or evidence that justifies the change.

## Candidate and publication handoff

```text
candidate_plan_ref:
approval_event:
approved_by_role:
approval_authority_source:
successor_publication_id:
successor_carrier_commit:
publication_required: yes
```

The approval binds the exact candidate. Publication must be validated under predecessor accepted governance and must advance the configured publication ref non-force from the exact incumbent carrier.

## Validation checklist

- [ ] Baseline publication identities come from validated publication-ref history.
- [ ] Candidate does not use its own new governance/authority to validate or authorize its transition.
- [ ] Plan declares intended grammar and nesting compatibility/migration impact.
- [ ] Every node uses a defined class.
- [ ] Every solid dependency is a true hard prerequisite.
- [ ] Every dotted scheduling edge is labeled exactly `preferred before`.
- [ ] OR/N-of-M logic uses an explicit Gate.
- [ ] Every Decision has exactly one deciding Role.
- [ ] Every active Milestone has exactly one primary assigned Role.
- [ ] Every Milestone has exactly one status class.
- [ ] Every newly projected DONE Milestone indexes a valid prior acceptance receipt.
- [ ] DONE receipt binds exact pre-acceptance contract PlanRef, evidence, and valid acceptance authority.
- [ ] Materially changed Milestone contracts do not silently inherit old acceptance.
- [ ] Issued acceptance receipts remain immutable history.
- [ ] Non-DONE status changes use appropriate execution/pause/resume evidence without fabricated acceptance.
- [ ] Child changes remain within parent authority/contract.
- [ ] Active-work impact is explicit.
- [ ] Candidate approval binds exact candidate SHA.
- [ ] Successor carrier parent and `CURRENT.prior_*` match the actual incumbent carrier.
- [ ] Publication ref advancement is non-force from that exact incumbent; stale sibling/replay is rejected.
- [ ] Propagation payload binds exact publication transition identities and occurs only after valid publication.