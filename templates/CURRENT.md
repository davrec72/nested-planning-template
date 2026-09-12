# Current accepted plan publication

Instantiate this file as:

```text
planning/CURRENT.md
```

Do not leave placeholders in an operational project.

```text
publication_protocol: plan-publication-v1
publication_id: <stable unique ID>
plan_id: <PlanID>
grammar: <grammar declared by plan_ref>
plan_ref: <exact accepted planning commit SHA>
prior_plan_ref: <previous accepted PlanRef or none>
prior_publication_id: <previous publication ID or none>
prior_publication_commit: <commit carrying previous planning/CURRENT.md or none>
approval_basis: role | founding | parent
approval_event: <durable locator proving approval of plan_ref>
approved_by_role: <RoleID or none>
approval_authority_source: <accepted source or none>
founding_record: <durable locator or none>
parent_authority_source: <durable locator or none>
publisher_identity: <attributable identity>
publication_authority_source: <source authorizing the publication action>
published_at: <timestamp or durable event time>
```

## Interpretation

- `plan_ref` is the current accepted planning state.
- This file is an index/publication record. The commit that writes this file is not automatically `plan_ref`.
- `prior_*` fields form the publication predecessor chain.
- `approval_basis=role` is the ordinary steady-state path.
- `approval_basis=founding` is valid only for the first publication of a root project under `planning/PUBLICATION.md`.
- `approval_basis=parent` is valid only for a child bootstrap whose accepted parent authority creates the child boundary.
- Fields that do not apply must contain `none`, not disappear.

Before publishing a replacement, verify that `prior_publication_id` and `prior_plan_ref` still equal the current valid record. If they do not, stop: the proposal is stale.

Do not edit an old publication record in history. Publish a new record that chains from the prior one.