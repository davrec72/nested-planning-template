# DATA definition template

Use for a node explicitly adopting `data-dependency-v1` under `planning/NODE_CONTRACTS.md`. Index this definition in `PLAN.md`. DATA describes an artifact dependency with objective usability; it has no Milestone acceptance or DONE class.

```text
plan_id: <PlanID>
data_id: <stable local DataID>
data_dependency_contract: data-dependency-v1
description: <the required evidence/artifact>
required_subject_and_input_revisions: <exact revisions or explicit deterministic binding rule>
artifact_identity_requirements: <exact artifact identity or deterministic resolution rule>
availability_alone_suffices: yes | no
objective_usability_predicate: <complete objective conditions>
current_resolution: none | <exact usable resolution ID/content identity/retained locator>
last_resolution_change: none | <exact usable or withdrawal record>
resolution_history: <retained history index or none before any resolution>
```

## Predicate and use

List objectively testable requirements, how each is checked, and freshness/validity windows if applicable. Keep artifact identity separate from the subject/input revisions the artifact describes. State how the consumer's exact required revisions are compared to the resolution.

Even when availability alone suffices, it means the required **exact artifact** for the specified subject/inputs. Missing/wrong-revision evidence cannot satisfy the node. The current accepted PlanRef must also index a valid resolution; artifact existence or a resolver's unindexed report alone is insufficient.

Use a Decision if selection or adequacy needs judgment. Use a Milestone if production itself is an outcome requiring acceptance. Do not hide either lifecycle in an unspecified DATA predicate.

## Resolution, replacement and withdrawal

Create an immutable record with `templates/DATA_RESOLUTION.md`. Index it only through accepted publication. Revalidate its exact artifact/subject/inputs and objective conditions at dispatch/use; no alternative resolution can substitute without accepted publication.

A replacement names the exact incumbent and becomes current only when the accepted PlanRef indexes it. A withdrawal preserves the incumbent in history, sets `current_resolution: none`, and indexes its withdrawal record in `last_resolution_change`. Each has an explicit authorized disposition for affected consumer work and preserves consumed evidence. Do not overwrite an old artifact/record to change what an old index means.
