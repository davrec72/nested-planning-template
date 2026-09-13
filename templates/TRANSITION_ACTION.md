# Transition-action manifest

Use only after explicit adoption of `transition-action-v1`, or as the predecessor-approved baseline evidence for its adoption. This adjunct leaves `plan-grammar-v2`, `plan-publication-v1`, publication-journal ordering and existing retention trust roots unchanged. See `planning/PUBLICATION_TRANSITIONS.md` for normative adoption, ordering and cold validation.

Prepare this immutable record at the configured path in the **successor publication carrier tree**, default `planning/TRANSITION_ACTION.md`. It need not be in the semantic candidate. It MUST NOT contain its own carrier SHA or its own blob hash. Preallocate stable publication, manifest, request/check and approval-event IDs before finalizing the content. The subsequent journal event binds the exact path, Git blob identity and record ID in the retained carrier. No PR/comment/history lookup is required to recover the actions.

## Exact transition and impact baseline

```text
transition_action_contract: transition-action-v1
transition_action_record_id: <unique immutable record ID>
plan_id: <PlanID with accepted repository/plan context>
publication_event_id: <preallocated stable journal event ID>
publication_id: <preallocated successor CURRENT publication ID>
accepted_predecessor_event_id: <last accepted event or none for bootstrap>
prior_plan_ref: <last accepted semantic PlanRef or none for bootstrap>
candidate_plan_ref: <exact candidate SHA; not this carrier>
semantic_delta: <complete accepted planning change or exact retained content>
execution_contract: none | <exact adopted execution contract/version and source>
execution_inventory_revision_or_snapshot: none | <exact serialized inventory revision/snapshot identity>
inventory_baseline_evidence: <exact analyzed snapshot/obligation set and predecessor-valid serialized mechanism>
publication_fence_id: <preallocated stable ID; none only for the permitted no-execution bootstrap>
publication_fence_scope: <exact coordination domain/plan/scope and all obligation-creating mutation entry points; or explicit bootstrap no-active basis>
legacy_reconciled_through_event_id: none | <predecessor high-water at adoption>
active_work_impact: none | explicit
no_impact_basis: none | <checked inventory analysis or explicit no-active-execution basis>
affected_attempts: [] | <entries below>
action_authority_source: <independently valid authority and exact source revision for these actions>
transition_action_approval_event: <preallocated ID/locator of durable approval binding this exact manifest>
```

For cross-plan objects use `qualified-reference-v1` after its accepted adoption; keep exact external authority revisions separate. The candidate's revision cannot authorize its own action manifest. Each action may cite its more specific predecessor-valid authority below.

Retain the exact inventory baseline and analysis needed to check completeness, including known outstanding attempts/legacy obligations and why other entries are unaffected. These may be inline or exact content objects in the same retained carrier tree; name their path/blob identity when separate. Include the source inventory revision, exact obligation set and configured serialization/fence basis. Fence scope must cover potential affected attempts and all paths that could create/broaden obligations, not only listed workers. Merely naming a mutable inventory URL, old chat or worker's current state is insufficient. This uses the existing carrier retention contract, not a new external retention trust root.

After approval, conditionally acquire the durable named fence against the exact analyzed baseline using the same mechanism as dispatch/inventory claims, before ref movement. Changed baseline means stop/rebuild/reapprove. Hold through the valid trusted journal commit; all affected obligation-creating/broadening mutations check the current fence through that same serialization and block while held. Pure observations/reductions are permitted only when they cannot broaden obligations. A plain reread is not equivalent.

Actual acquisition/held-through-commit evidence is bound by the existing trusted journal event to this ID/scope/baseline and exact manifest/candidate identities. It is not inserted into an already-approved manifest; preallocated IDs avoid approval/self-reference cycles. Success releases only after commit. Failure/uncertain ref movement or retention/journal failure preserves the durable fence until the explicit abort/recovery rules in `planning/PUBLICATION_TRANSITIONS.md` section 9 permit release; timeout is insufficient.

## Affected attempts

Use one entry for each exact affected package revision/attempt. Each entry lists every independently obligated recipient for that attempt; a mere transit hop is not another obligation. Missing entries are not implicit `continue`.

```text
work_package_id: <stable package ID, qualified when cross-plan>
package_revision: <immutable exact revision>
attempt_id: <exact attempt>
authorization_id: <exact existing execution grant/source>
target_type: milestone | decision | data | plan-maintenance
target_id: <exact local/qualified target>
target_record: <exact accepted target definition>
disposition: continue | pause | redirect | supersede
exact_affected_scope: <bounded actions/resources/in-flight work to reconcile>
action_authority_source: <predecessor-valid source covering this attempt/action>
recipient_obligations: <one or more entries below>
```

For every obligated recipient record:

```text
request_id: <preallocated stable request ID, reused on reconstruction>
requested_action: continue | pause | revoke | reduce-scope | redirect | supersede
requested_action_payload: <complete exact instructions, destination/changed bounds and conditions; none only when action/scope is complete without extras>
obligated_recipient_identity_context: <exact identity and execution context>
recipient_action_scope: <exact obligation within the affected scope>
initial_preferred_routes_or_resolution_rule: <supported routes or exact deterministic rule with retained inputs>
acknowledgement_deadline_rule: <absolute time or finite timeout with exact event/time anchor>
application_deadline_rule: <absolute time or finite timeout with exact event/time anchor>
recovery_check_obligations: <stable logical IDs, owners/authority, purpose, finite triggers and required verification>
retry_query_fallback_escalation: <bounded actions and exact supported routes/authority>
supersedes_request: none | <exact predecessor request and explicit authorized disposition>
```

Rules must suffice to reconstruct the same request, scope, recipient, deadlines and recovery obligations without interpretation of notification prose. For example, acknowledgement may be due one minute after the journal event's `committed_at`, with application due two minutes after the exact acknowledgement. Preserve resolved timestamps; discovery/retry never restarts a deadline. Already overdue obligations require immediate authorized recovery, not a fresh timeout window. Retain the exact anchor evidence. A missing/ambiguous rule blocks the affected transition/reconciliation.

Bind any proposed redirect destination or successor scope to its exact prior/candidate definition and permitted action payload. Activation still waits for accepted publication and any independently required executor grant/revalidation; the manifest does not authorize a fresh executor or silently rewrite an immutable package.

Preallocated logical check IDs identify obligations, not a claim that a scheduler task exists. After acceptance, Foreman records actual verified task IDs/owners and evidence in the inventory. Failed verification remains a recovery blocker.

One receipt key remains `request_id` + obligated recipient identity/context + `work_package_id` + `package_revision` + `attempt_id` within project/plan context. Direct, fallback, retry, webhook and prompt routes are retained transport attempts inside it. The carrier/journal identities come from the validated event when the receipt is synthesized; the manifest never needs its own future carrier SHA. Replay reuses the same request/receipt/check obligations and does not duplicate dispatch. Closure reconciles the obligation or valid supersession, not every route's success.

## Explicit no impact and approval

Every adopted bootstrap/normal/recovery planning publication carries a manifest. A checked no-impact transition uses `active_work_impact: none`, `affected_attempts: []`, and the exact protected inventory baseline/no-impact analysis. An adopted inventory still requires a fence for no impact. Only a first root/child publication with no pre-existing dispatch-capable execution system may use execution/inventory/fence `none` and an explicit no-active-execution basis. Legacy active/still-dispatchable work needs predecessor-valid exclusion under section 9; lack of an adopted inventory alone is not an exception. Unknown active work cannot be called none. An affected attempt deliberately grandfathered into the successor must be listed as `continue`, with its explicit recipient/action/recovery obligations.

Finalize the manifest, compute its blob identity, then obtain predecessor-valid approval explicitly binding that identity, record ID and exact candidate. The manifest may refer to a preallocated approval-event ID; that event is issued afterward against the final blob, avoiding a content-hash cycle. The candidate approval can be reused only if it explicitly binds both exact objects. Otherwise obtain a separate valid manifest approval. Retain sufficient approval evidence with the carrier or trusted journal under the existing approval/publication trust rules; a PR/comment locator or unauthenticated copied claim alone is insufficient. A changed blob or candidate requires new applicable approval; an ID alone is not proof of approval.
