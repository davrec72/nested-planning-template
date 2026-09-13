# Immutable DATA resolution template

Use under `data-dependency-v1`. Issued records are immutable; replacement/withdrawal uses a new ID and exact predecessor link. Resolution evidence is not Milestone acceptance, and becomes eligible for use only when selected by the current accepted published PlanRef.

```text
resolution_id: <unique stable ID>
plan_id: <PlanID>
data_id: <DataID>
data_dependency_contract: data-dependency-v1
record_kind: usable | withdrawal
data_contract_plan_ref: <exact accepted SHA containing the definition resolved>
data_definition_locator: <exact definition at that SHA>
subject_and_input_revisions: <exact subject/input identities, distinct from artifact identity>
artifact_locator: <retrievable exact artifact; for withdrawal identify prior artifact>
artifact_identity: <exact version/digest/object ID>
resolution_rule_and_inputs: <exact rule evaluation, or none for directly pinned identity>
predicate_evaluation_and_evidence: <exact check evidence; withdrawal reason/evidence when withdrawn>
resolved_by: <resolver identity/context and applicable existing execution authority>
resolved_at: <time/durable event>
prior_resolution_change: none | <exact accepted last_resolution_change>
supersedes_resolution: none | <exact incumbent usable resolution for replacement>
withdraws_resolution: none | <exact incumbent usable resolution for withdrawal>
affected_consumer_work_disposition: <exact disposition record/table below>
```

## Objective evidence

| Required condition | Exact observation/evidence | Result |
|---|---|---|
| `<identity, subject, availability or other declared criterion>` | `<retained evidence>` | `<satisfied / failed / unavailable>` |

A `usable` resolution requires all declared conditions to be satisfied for the required subject/inputs. Failed/unavailable observations are evidence, not a usable resolution. A withdrawal documents why the previous resolution must no longer be selected and does not claim a usable replacement artifact.

Validate `prior_resolution_change` against the accepted predecessor. First issuance uses `none`; renewal after withdrawal needs a new usable resolution naming the withdrawal and current predicate evidence. Do not silently reindex the withdrawn record. If the record remained selected and only availability failed temporarily, recheck restored availability under the existing selection.

## Consumer work disposition

| Affected consumer / exact work revision | Continue / pause / supersede | Existing authority | Evidence retention / remaining effects |
|---|---|---|---|
| `<consumer/package/revision>` | `<disposition>` | `<source>` | `<record>` |

Use `none` only with evidence of no affected consumers. Retain old resolution/consumption history; old identity cannot silently become the new artifact. Continued work remains bounded by its independent authority and explicit disposition.

## Activation handoff

An authorized plan change indexes the exact usable resolution or withdrawal through the existing publication/journal/retention protocol. The later indexing PlanRef does not replace `data_contract_plan_ref`. At use, check exact current selection, artifact identity, required subject/inputs and objective usability again. Record the exact resolution/artifact consumed in returned evidence.
