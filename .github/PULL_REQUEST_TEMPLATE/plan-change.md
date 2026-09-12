## Semantic delta

Describe the planning meaning that changes. Do not merely describe the file diff.

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

If yes, provide the propagation payload Foreman should receive after merge.

## Parent/child impact

```text
parent_contract_changed: yes | no
child_plan_changed: yes | no
parent_notification_required: yes | no
```

## Controlling decision / evidence

Link the accepted decision, delegation, or evidence that justifies the change.

## Validation checklist

- [ ] Every node uses a defined class.
- [ ] Every solid dependency is a true hard prerequisite.
- [ ] Every dotted scheduling edge is labeled exactly `preferred before`.
- [ ] OR/N-of-M logic uses an explicit Gate.
- [ ] Every Decision has exactly one deciding Role.
- [ ] Every active Milestone has exactly one primary assigned Role.
- [ ] Every Milestone has exactly one status class.
- [ ] No proposed edit bootstraps its own authority.
- [ ] Child changes stay within the parent contract or parent authority is included.
- [ ] Active-work impact is explicit.
- [ ] Foreman propagation is defined if needed.
