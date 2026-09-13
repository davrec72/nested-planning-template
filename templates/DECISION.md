# Decision definition template

Use for a node explicitly adopting `decision-result-v1` under `planning/NODE_CONTRACTS.md`. Index this definition in the plan's `PLAN.md`; fill every required semantic field before adoption/dispatch. The accepted definition references existing authority and cannot create it.

```text
plan_id: <PlanID>
decision_id: <stable local DecisionID>
decision_result_contract: decision-result-v1
question: <actual question/choice>
deciding_role: <the unique Role on the decides edge>
decision_authority_source: <independently accepted source covering this judgment>
input_requirements: <exact required inputs or explicit revision-binding rule>
selection_cardinality: exactly_one | one_or_more
active_result: none | <exact immutable selection ID/content identity/retained locator>
last_result_change: none | <exact selection or revocation record>
result_history: <retained history index, or none before any result>
```

## Outcomes and prerequisites

| Stable outcome token | Meaning | Outgoing destination(s) |
|---|---|---|
| `<token>` | `<precise result meaning>` | `<node IDs or explicitly no downstream branch>` |

Label each materially distinct outgoing path with its token. State the Decision's own prerequisite/input evidence and where it is verified. Multiple ordinary incoming hard prerequisites remain AND. An alternative rejoin requires an explicit objective OR Gate; define whether it counts only currently selected outcomes.

## Current result and changes

Produce an immutable result using `templates/DECISION_RESULT.md`. Research or an unindexed result opens no branch. A later accepted published PlanRef must index the exact result here before it becomes operative. That indexing PlanRef does not replace the result's original definition/input PlanRef.

Replacement/revocation names the exact prior active result, preserves it, and supplies an explicit authorized disposition for affected branch work. Replacement indexes the new selection; revocation sets `active_result: none` and indexes the revocation in `last_result_change`. Do not silently flip a token, edit an issued result, or activate a record from a mutable branch.
