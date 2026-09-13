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

Use the [canonical plan-change template](../../templates/PLAN_CHANGE.md#active-work-handling) and [execution recovery contract](../../planning/EXECUTION.md#lost-requests-and-continued-execution) at the exact accepted PlanRef. After reconciling the configured inventory, state `none` only if no attempt is affected; otherwise repeat this block for **each exact package revision/attempt**:

```text
work_package_id:
package_revision:
attempt_id:
target_type:
target_id:
target_record:
requested_action: continue | pause | revoke | reduce-scope | redirect | supersede
exact_affected_scope:
recipient_identity_context:
recipient_route:
acknowledgement_due_at:
application_due_at:
recovery_check_obligation: <owner, trigger/deadline, recovery action and fallback/escalation route>
```

Before publishing a material pause/revoke/scope-reduction/redirect/supersede change, complete each affected attempt's deadlines and recovery/check obligation. A missing worker is not stopped; prior accepted planning state governs until trusted publication succeeds.

## Authority impact

```text
none | binding change | scope change
```

If authority changes, cite authority valid before this candidate.

## Foreman dispatch required

Managed execution requires current accepted `transition-action-v1`, its exact configured carrier path, valid adoption/legacy-baseline reconciliation and verified required checks, with no reconciliation failure blocking the action. `none` permits planning/inventory/read-only coordination, not first/later dispatch/start/resume or obligation-creating attempts/rebindings. A propagation wake is not permission to create an executor obligation.

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

Apply the [operational eligibility boundary](../../planning/PUBLICATION.md#operational-execution-eligibility). A material publication remaining in `none` must affect no active/outstanding execution obligation and remain no-dispatch. Legacy active/outstanding work blocks material alteration until valid prior-authorized stop/reconciliation or conforming adoption. For adoption, first prevent new obligations and reconcile the complete legacy set, then publish the approved baseline manifest/fence; enable dispatch only after the adopting event/carried obligations are indexed/reconciled with checks verified.

When `transition-action-v1` applies, including its explicitly approved adoption baseline, prepare the [immutable transition-action manifest](../../templates/TRANSITION_ACTION.md) before approval. Preserve the full impact/inventory analysis and per-attempt recipient/action/deadline/recovery data in the successor carrier, including explicit `continue` or a checked empty manifest. The PR is not reconstruction storage.

```text
candidate_plan_ref:
transition_action_contract: none | transition-action-v1
prior_transition_action_contract:
adoption_baseline_reconciliation_and_eligibility_evidence:
transition_action_path_blob_and_record_id:
execution_inventory_revision_or_snapshot:
publication_fence_id:
publication_fence_scope:
publication_fence_acquisition_and_held_through_commit_evidence:
legacy_reconciled_through_event_id:
transition_action_approval_event:
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

For the adjunct, predecessor-valid approval binds the exact candidate and manifest, including analyzed baseline and preallocated fence ID/scope. After candidate retention/carrier creation, conditionally acquire that durable fence through the same serialized inventory/dispatch mechanism before ref movement; changed baseline requires rebuild/reapproval. Block affected obligation-creating/broadening mutations through carrier retention and valid journal commit. The trusted event binds exact manifest and fence ID/scope/baseline/acquisition/continuity evidence. Normal release follows commit; a plain reread cannot substitute.

Follow [section 9](../../planning/PUBLICATION_TRANSITIONS.md#92-ordering-and-inventory-completeness) for verified pre-ref abort, held-fence recovery or abort/suffix reconciliation after ref movement, and failed release after commit. Timeout cannot erase a fence. A later publication after abort/release needs fresh baseline/manifest/approval/fence. No-impact still fences an adopted inventory; bootstrap/legacy exceptions require the explicit predecessor-valid basis.

## Post-publication execution evidence

After trusted journal commit, durably record/index a [request and recipient receipt](../../templates/EXECUTION_RECEIPT.md) for each affected attempt before its wake. Bind the committed event; verify the acknowledgement/application checks before relying on the request. Complete or link the per-attempt evidence:

For adopted publications, validate and reconstruct from that event's exact retained manifest, reusing its request/check identities and anchored deadlines. Advance the publication-reconciliation marker only after the complete obligation set is indexed/reconciled with checks verified. A valid explicit empty manifest creates no receipts; notification prose cannot replace missing manifest evidence.

```text
publication_event_id:
request_receipt_and_inventory_locators:
actual_verified_check_ids_owners_and_triggers:
acknowledgement_evidence:
application_or_enforcement_evidence:
remaining_unstopped_scope_and_recovery:
```

Track recorded, sent/wake attempted, delivered, acknowledged, applied and closed separately. **Sent, delivered or acknowledged does not establish paused / confirmed stopped.** Require cessation/application or verified enforcement evidence covering the exact scope and in-flight work; keep unresolved or partially stopped scope outstanding with recovery checks. Follow the [canonical propagation requirements](../../templates/PLAN_CHANGE.md#foreman-propagation-payload), including verified publication reconciliation when the initial notification is lost.

## Dependency conformance

Link the [bounded satisfiability analysis](../../planning/SATISFIABILITY.md) for the exact candidate and affected prerequisite/consumer scope: current PlanRefs/events, actual seeds, operative Decision selections, explicit Gate sufficient-input sets, finite witness or residual cycle/condition/unknown blockers, deferred scope and next-action readiness. Candidate feasibility does not open current prerequisites or supply approval. Retain the full analysis with normal change evidence under [PLAN_CHANGE](../../templates/PLAN_CHANGE.md#dependency-conformance).

## Validation checklist

- [ ] Baseline identities come from the trusted publication journal.
- [ ] `none` is no-dispatch and affects no outstanding execution obligation through this material change; any operational adoption has prior-authorized legacy reconciliation and dispatch waits for its indexed baseline/verified checks.
- [ ] Candidate does not use its own new governance/authority to validate or authorize its transition.
- [ ] Plan declares intended grammar and nesting compatibility/migration impact.
- [ ] Every node/edge obeys the accepted planning grammar.
- [ ] Dependency conformance rejects self-dependencies/unavoidable unmet cycles, respects Gate predicates and operative Decision branches, and excludes assignment/authority/preferences; no blocked/unknown scope is claimed dispatchable.
- [ ] Actual next-action prerequisites and full ancestor readiness are checked separately from hypothetical feasibility; changes to relevant state/selections revalidate the analysis.
- [ ] Every active Milestone has one primary assigned Role and one status class.
- [ ] DONE projections index valid prior acceptance; non-DONE status changes use appropriate execution evidence.
- [ ] Child changes remain within parent authority/contract.
- [ ] Impact, typed target and recipient/route are recorded per exact affected package revision/attempt.
- [ ] Material-action deadlines and recovery/check obligations are complete before publication.
- [ ] Candidate approval binds exact candidate SHA.
- [ ] When the adjunct applies, predecessor-valid approval also binds the exact manifest blob/record ID, with complete inventory analysis and explicit affected `continue` or checked no impact.
- [ ] Conditionally acquired durable fence matches the approved baseline/ID/scope; changed baseline causes rebuild/reapproval. Same-mechanism dispatch/mutation guards exclude new/broadened obligations through valid journal commit.
- [ ] Fence acquisition/continuity/release or explicit abort/recovery evidence is durable; no-impact/bootstrap/legacy handling follows section 9 and no timeout clears an ambiguous fence.
- [ ] Exact candidate is durably retained and cold-fetchable independently of ordinary branches.
- [ ] For normal publication, actual carrier parent equals the last accepted carrier.
- [ ] For recovery, actual carrier parent and accepted predecessor are separately recorded; invalid suffix remains preserved/non-accepted.
- [ ] Publication ref movement is conditional/non-force from the exact actual tip.
- [ ] Trusted journal receives durable `ref_update_receipt` and exact transition identities.
- [ ] Every adopted carrier retains its manifest/inputs, and the journal binds exact path/blob/record ID and inventory-validation evidence; legacy adoption/history rules are explicit.
- [ ] Publication is not current until trusted journal event commits.
- [ ] Propagation payload binds the committed publication event and occurs only afterward.
- [ ] Post-publication requests/receipts are durably indexed and acknowledgement/application checks are verified, with evidence or unresolved obligations recorded per attempt.
- [ ] No sent/delivered/acknowledged stop is labeled paused or confirmed stopped without cessation/enforcement evidence for its scope and in-flight work.
