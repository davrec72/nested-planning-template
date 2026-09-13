# Immutable Decision result template

This record captures a judgment or its explicit revocation under `decision-result-v1`; it is not operative until indexed by the current accepted published PlanRef. Do not edit an issued record or reuse its ID for different content. Use a new linked record for replacement/revocation.

```text
result_id: <unique stable result ID>
plan_id: <PlanID>
decision_id: <DecisionID>
decision_result_contract: decision-result-v1
record_kind: selection | revocation
decision_contract_plan_ref: <exact accepted SHA containing the definition judged>
decision_definition_locator: <exact definition at that SHA>
input_revisions: <exact subjects/inputs/evidence revisions actually judged>
authority_state_plan_ref: <exact accepted authority state at issuance>
deciding_role: <unique deciding Role with existing authority>
decision_authority_source: <exact independent authority source>
issuing_holder_and_binding: <issuer identity and accepted current Role/holder binding>
issued_at: <time/durable issuance event>
selected_outcomes: <distinct declared tokens; empty only for revocation>
selection_cardinality: <exact rule from the accepted Decision definition>
evidence_and_rationale: <exact retained evidence plus reasoning locator>
prior_result_change: none | <exact accepted last_result_change>
supersedes_result: none | <exact incumbent selection for replacement>
revokes_result: none | <exact incumbent selection for revocation>
affected_branch_work_disposition: <exact disposition record/table below>
```

## Determination

State the answer and why the evidence supports the selected outcome(s). Verify the Decision's own prerequisites, input requirements, current deciding authority and selection cardinality. A result cannot change the question, permitted outcomes, authority or input requirements it is supposed to judge.

For revocation, state the exact prior result and revocation reason/evidence. This closes selection through the later accepted index change; it does not choose an alternative outcome.

Validate `prior_result_change` against the accepted predecessor. First issuance uses `none`; after revocation, reactivation is a new selection naming that revocation, not silent reindexing of an old result. An unchanged active result can remain selected across unrelated publications without being reissued.

## Branch work disposition

| Affected old outcome / exact work revision | Continue / pause / supersede | Existing authority | Rationale / retained evidence / remaining effects |
|---|---|---|---|
| `<token; package/work/revision>` | `<disposition>` | `<source>` | `<record>` |

Use `none` only with evidence that no affected work exists. Continued old-branch work must be named and independently authorized; it does not reopen that branch for new dispatch. Account for downstream consumers/rejoins when their assumptions change. An unresolved disposition prevents activation publication; record existence is not proof of stopping work.

## Activation handoff

The plan change validates this exact record against the current compatible definition, names the exact incumbent it replaces/revokes, and indexes its new state under `planning/NODE_CONTRACTS.md`. It then follows the existing publication/journal/retention protocol. Do not edit this record to insert the later activation PlanRef. Preserve its issuance identity, original contract PlanRef and evidence.
