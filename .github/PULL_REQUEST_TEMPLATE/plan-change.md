## Semantic delta

Describe planning meaning, not merely file diff.

## Accepted baseline

Resolve from trusted publication-journal state:

```text
publication_ref:
publication_journal_high_water_event_id:
accepted_predecessor_commit:
prior_publication_id:
prior_plan_ref:
```

Do not use newest branch/ref content as accepted state.

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

Do not propagate the candidate merely because it merges or the publication ref moves. Propagation begins only after the trusted publication-journal event commits.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

## Controlling decision / evidence

Link the accepted decision, delegation, or evidence that justifies the change.

## Candidate / retention / publication handoff

```text
candidate_plan_ref:
approval_event:
approved_by_role:
approval_authority_source:
plan_snapshot_locator:
plan_snapshot_retention_evidence:
transition_kind: bootstrap | normal | recovery
accepted_predecessor_event_id:
accepted_predecessor_commit:
carrier_parent_commit:
successor_publication_id:
successor_carrier_commit:
ref_update_receipt:
publication_journal_event_id:
publication_required: yes
```

## Validation checklist

- [ ] Baseline identities come from the trusted publication journal.
- [ ] Candidate does not use its own new governance/authority to validate or authorize its transition.
- [ ] Plan declares intended grammar and nesting compatibility/migration impact.
- [ ] Every node/edge obeys the accepted planning grammar.
- [ ] Every active Milestone has one primary assigned Role and one status class.
- [ ] DONE projections index valid prior acceptance; non-DONE status changes use appropriate execution evidence.
- [ ] Child changes remain within parent authority/contract.
- [ ] Active-work impact is explicit.
- [ ] Candidate approval binds exact candidate SHA.
- [ ] Exact candidate is durably retained and cold-fetchable independently of ordinary branches.
- [ ] For normal publication, actual carrier parent equals the last accepted carrier.
- [ ] For recovery, actual carrier parent and accepted predecessor are separately recorded; invalid suffix remains preserved/non-accepted.
- [ ] Publication ref movement is conditional/non-force from the exact actual tip.
- [ ] Trusted journal receives durable `ref_update_receipt` and exact transition identities.
- [ ] Publication is not current until trusted journal event commits.
- [ ] Propagation payload binds the committed publication event and occurs only afterward.
