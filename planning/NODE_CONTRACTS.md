# Decision and DATA contracts

This file defines the separately versioned `decision-result-v1` and `data-dependency-v1` contracts. They supplement `plan-grammar-v2`; they do not add node classes, arrow syntax, Milestone statuses, or a second publication system.

An instantiated plan explicitly adopts a contract by indexing a node definition that declares its version in the **accepted published PlanRef**. Keep a discoverable node-contract index in that plan's `PLAN.md`. Missing/unsupported declared contracts or unavailable required records block the affected node/boundary. Do not infer a version from a diagram's appearance.

## Currentness and exact records

Use the current accepted PlanRef established by `PUBLICATION.md` and `PUBLICATION_TRANSITIONS.md` as the sole operative selection boundary. That snapshot's node definition indexes the exact active Decision result or DATA resolution. A newer file, issue comment, branch, timestamp, notification or durable but unindexed record cannot replace that selection.

The plan's node index, definition identity/version, current record and last-change record must agree. A selection/usable last-change record must be the current indexed record; a revocation/withdrawal last-change record requires an empty current index. Initially both are `none`. Contradictory fields or duplicate definitions do not create alternative sources of currentness; stop the affected dependency and resolve them through accepted governance.

Definitions and their current indices are accepted planning state. Issued result/resolution/change records are immutable history. Retain exact records, including the history necessary to validate replacement/withdrawal, either in retained planning snapshots or through explicit durable locators with content identity. A locator that resolves to editable text without exact identity is insufficient. When copying an issued record into a later retained snapshot, preserve its exact contents and original issuance bindings. Missing required evidence fails closed at the affected dependency; an index cannot supply the missing evidence.

A record binds the exact accepted PlanRef containing the definition it judged/resolved, plus exact subject/input revisions. A later snapshot that indexes that record is not substituted for its original contract/input PlanRef. The later snapshot must retain compatible semantic definition fields: node identity, question/predicate, outcomes/cardinality where applicable, required subjects/inputs, prerequisites and authority scope. Index/history changes alone do not re-judge the contract. Material definition/input changes require a new record against the applicable accepted definition; old evidence cannot silently migrate to a new meaning.

If a changed definition must become accepted before a new record can be issued, publish that definition with an empty current index and explicit authorized deactivation/work disposition for the old record, retaining its history. Then issue against the accepted definition and publish activation. Do not keep an incompatible old record operative or treat the candidate definition as already accepted.

Selecting/replacing/deactivating an operative record is a plan change. Validate the candidate under the accepted predecessor governance, obtain the independently required approval, retain/publish it through the existing journal protocol, and then propagate its explicit work impact. Indexing a record cannot create substantive authority, waive prerequisites, or weaken a parent contract.

## `decision-result-v1`

Use `templates/DECISION.md` and `templates/DECISION_RESULT.md`.

### Decision definition

Every adopting Decision has a durable definition with at least:

```text
plan_id
decision_id
decision_result_contract: decision-result-v1
question
deciding_role
decision_authority_source
input_requirements
outcomes: <stable outcome tokens and their meanings/edge mappings>
selection_cardinality: exactly_one | one_or_more
active_result: none | <exact selection record identity and retained locator>
last_result_change: none | <exact selection/revocation record>
result_history: <retained record index>
```

`deciding_role` must match the unique incoming `decides` edge and independently possess the stated decision scope. The definition references authority; it cannot grant it. Actual required input revisions are pinned in the result, and must satisfy the definition's input requirements and the Decision's own prerequisites.

Outcome tokens are unique, stable identifiers within this Decision. Each materially distinct outgoing Decision path is labeled with its exact outcome token. A display description may explain a token but cannot silently rename its meaning. A selection contains a nonempty set of distinct declared tokens: `exactly_one` requires one; `one_or_more` permits any nonempty subset. If a project needs another cardinality/selection rule, it must define and explicitly adopt compatible contract semantics before using it; do not invent an unstated default.

### Issuing and activating a result

A selection record binds at least:

```text
result_id
plan_id
decision_id
decision_result_contract: decision-result-v1
record_kind: selection | revocation
decision_contract_plan_ref
decision_definition_locator
input_revisions
authority_state_plan_ref
deciding_role
decision_authority_source
issuing_holder_and_binding
issued_at
selected_outcomes
selection_cardinality
evidence_and_rationale
prior_result_change: none | <exact last_result_change in the accepted predecessor>
supersedes_result: none | <exact prior active selection>
revokes_result: none | <exact prior active selection>
affected_branch_work_disposition
```

The issuing holder validates its accepted authority/current binding at issuance. Merely naming the deciding Role, producing research, or writing a result file does not issue that Role's judgment. A holder later leaving the Role does not rewrite an already issued result; current use remains subject to the indexed result, current compatible definition and any accepted replacement/revocation.

At first issuance, all three predecessor fields are `none`. Every later record names the exact accepted `last_result_change` in `prior_result_change`, including activation after revocation. Publication may activate the selection only after verifying its exact predecessor, contract/inputs, Role authority, outcome membership/cardinality, retained evidence and work disposition. In the successor PlanRef set `active_result` and `last_result_change` to that exact selection, retaining its original definition/input/authority bindings.

Until this publication, `active_result: none` opens no outgoing Decision branch. Once operative, a labeled Decision edge is satisfied **only** when its token is in the indexed valid selection. Unselected outcome edges are closed for new dispatch. Selecting an edge is only one prerequisite: every other hard prerequisite of its destination and ordinary authority constraints still applies. A Decision does not acquire a Milestone DONE class or acceptance receipt.

### Replacement, revocation and active work

A replacement is a new immutable selection whose `supersedes_result` names the exact incumbent, with `revokes_result: none`. A revocation is a new immutable `record_kind: revocation` record whose `revokes_result` names the exact incumbent and `supersedes_result` is `none`; its `selected_outcomes` is empty as a revocation, not an invalid empty selection. Preserve the prior selection and its evidence. A competing record that does not name the current incumbent cannot win by recency; reconcile it through a new authorized change.

The accepted successor PlanRef must explicitly record the predecessor's deactivation. For replacement, index the new selection as active; for revocation, set `active_result: none` and index the revocation in `last_result_change`. Preserve both in `result_history`. Unpublished replacements/revocations do not alter operative branches. Evidence that the current selection's required conditions cannot be validated still blocks dependent dispatch; this does not activate an alternative result.

After revocation, reactivation requires a new authorized immutable selection naming that revocation as `prior_result_change`, with no active result to supersede/revoke, fresh applicable evidence and explicit work disposition. Do not silently reindex a previously deactivated selection. Carrying the same still-active record forward across an unrelated publication is not reactivation.

Every replacement/revocation includes an explicit disposition for each affected old-branch package/outcome: `continue`, `pause`, or `supersede`, with exact work/revision identity, rationale, independent authority and retained-evidence handling. `none` is permitted only with evidence that no affected work exists. A `continue` disposition can cover named already-authorized work; it does not reopen the old branch for new dispatch, authorize wider scope, or assert the old branch still satisfies a current rejoin. If required work disposition/authority is unresolved, do not publish the activation change. Foreman coordinates application under the accepted propagation contract; record selection alone does not prove physical work stopped.

Multiple incoming edges to an ordinary downstream node still mean AND. Alternative branch rejoining therefore requires an explicit objective OR Gate. If only outcomes selected by the **current** result should count, state that in the Gate predicate; an old branch's historical DONE projection does not silently count as a currently selected branch. See `examples/node-lifecycle/README.md`.

## `data-dependency-v1`

Use `templates/DATA.md` and `templates/DATA_RESOLUTION.md`.

### DATA definition

Every adopting DATA node has a durable definition with at least:

```text
plan_id
data_id
data_dependency_contract: data-dependency-v1
description
required_subject_and_input_revisions
artifact_identity_requirements: <exact identity or explicit deterministic resolution rule>
availability_alone_suffices: yes | no
objective_usability_predicate
current_resolution: none | <exact usable resolution identity and retained locator>
last_resolution_change: none | <exact usable/withdrawal record>
resolution_history: <retained record index>
```

The required subject is the object/revision that the artifact describes, not the artifact's own revision. Keep both identities. `required_subject_and_input_revisions` names exact revisions or an explicit deterministic binding rule that pins them for each use. A result for implementation X cannot satisfy a dependency requiring implementation Y merely because the report exists or passes its own checks.

The predicate must be objective and complete enough to evaluate: required format/content, provenance relationships, validity/freshness window when relevant, and any other project-specific usability conditions. An unspecified criterion is not automatically satisfied. `availability_alone_suffices: yes` means only availability of the **required exact artifact for the specified subject/inputs** is needed; it does not waive identity or current-resolution selection. If choosing between artifacts or deciding their adequacy requires judgment, model that judgment as a Decision. If completion of artifact production is the outcome to accept, use a Milestone. DATA itself gains no acceptance Role or DONE class.

### Resolution and use

A usable resolution is an immutable record containing at least:

```text
resolution_id
plan_id
data_id
data_dependency_contract: data-dependency-v1
record_kind: usable | withdrawal
data_contract_plan_ref
data_definition_locator
subject_and_input_revisions
artifact_locator
artifact_identity: <exact version/digest/object ID>
resolution_rule_and_inputs: <when applicable, otherwise none>
predicate_evaluation_and_evidence
resolved_by
resolved_at
prior_resolution_change: none | <exact last_resolution_change in the accepted predecessor>
supersedes_resolution: none | <exact prior current resolution>
withdraws_resolution: none | <exact prior current resolution>
affected_consumer_work_disposition
```

The resolver records objective evidence; it does not thereby accept a Milestone or issue a discretionary judgment. Producing the resolution and adopting it each need their own applicable existing execution/planning authority. A candidate plan cannot authorize its own adoption.

The successor accepted PlanRef may index the exact resolution only after verifying its definition, artifact identity, required subject/inputs, objective predicate evidence, and work impact. `current_resolution: none` is unsatisfied. A file existing, a resolver's claim, or an unindexed resolution is insufficient.

At dispatch/use, retrieve the indexed resolution and required exact artifact, match its subject/inputs to this consumer's requirements, and evaluate the stated objective conditions. Missing artifact, wrong identity/revision, or unmet/expired predicate means **unsatisfied**, even if a prior observation passed. The publication boundary chooses which resolution is eligible; current objective checks establish whether that selected evidence remains usable. A failed check cannot select another artifact or resolution outside the current PlanRef. Record the exact consumed resolution/artifact in returned evidence.

### Replacement and withdrawal

An initial usable resolution has all three predecessor fields `none`. Every later record names the exact accepted last change in `prior_resolution_change`. Replacement produces a new immutable usable resolution naming the exact incumbent in `supersedes_resolution`, with `withdraws_resolution: none`. After ordinary accepted publication, the new definition state indexes it in `current_resolution` and `last_resolution_change`; preserve the old record/history. A newer artifact or mutable URL cannot silently replace the old identity. Material subject/predicate changes first require their own accepted definition, then evidence/resolution against that definition.

Withdrawal produces a new immutable `record_kind: withdrawal` record naming the exact incumbent in `withdraws_resolution`, with `supersedes_resolution: none`, its reason/evidence and affected consumers. A withdrawal does not assert a usable new artifact. The successor accepted PlanRef sets `current_resolution: none`, indexes the withdrawal in `last_resolution_change`, and preserves all historical resolution records. An unindexed withdrawal proposal does not select new planning state; independently observed failed objective conditions still make the indexed artifact unusable.

After withdrawal, any renewed selection requires a new usable resolution naming the withdrawal as its prior change, no active resolution to supersede/withdraw, current predicate evidence and explicit consumer disposition. Repointing to a previously withdrawn record is not renewal. Restored objective availability of a record that remained selected is different: it needs rechecking, not a new selection record.

Both changes explicitly state affected consumer work disposition (`continue`, `pause`, or `supersede`), exact revisions, evidence retention and existing authority. Old evidence remains history; it cannot justify new dispatch as though its resolution were still current. Already active work requires its explicit bounded disposition; publication is not proof that tools have stopped. No DATA acceptance receipt or Milestone status projection is introduced.

## Adoption and compatibility

These are explicitly adopted node contracts, not a silent reinterpretation of all historical v2 nodes. New plans should use the provided versioned records. A legacy plan with explicit different Decision/DATA semantics continues under those accepted semantics until its migration becomes current; a missing contract cannot be repaired by guessing.

An adoption change must:

1. enumerate the affected nodes and their prior explicit semantics/operative state;
2. declare `decision_result_contract: decision-result-v1` or `data_dependency_contract: data-dependency-v1` in each adopting definition and index its exact definition/current records;
3. supply valid immutable result/resolution records under the accepted definition and authority, or adopt an explicit empty index until such records exist; do not backdate records or invent historical evidence;
4. state current branch/consumer work disposition and any changed dependency behavior;
5. preserve prior records/PlanRefs, obtain approval under preceding accepted governance, and publish through the existing journal/retention mechanism before using the new semantics.

A migration can first publish the adopted definition with an empty index, then issue a record against that accepted definition and publish its activation. It cannot use the candidate definition as already accepted. Unsupported versions fail closed at affected nodes/boundaries; shared `plan-grammar-v2` syntax alone does not prove node-contract compatibility. No automatic cross-plan mapping or global satisfiability rule is defined here.
