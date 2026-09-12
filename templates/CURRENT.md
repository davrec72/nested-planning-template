# Current accepted plan publication

Instantiate this file as `planning/CURRENT.md` on the configured publication ref (portable default `refs/heads/plan-publications`).

Do not leave placeholders in an operational project.

```text
publication_protocol: plan-publication-v1
publication_id: <stable unique ID>
plan_id: <PlanID>
grammar: <grammar declared by plan_ref>
plan_ref: <exact accepted planning commit SHA>
prior_plan_ref: <previous accepted PlanRef or none>
prior_publication_id: <previous publication ID or none>
prior_publication_commit: <exact predecessor publication carrier commit or none>
approval_basis: role | founding | parent
approval_event: <durable locator proving approval of plan_ref>
approved_by_role: <RoleID or none>
approval_authority_source: <accepted source or none>
founding_record: <durable locator or none>
parent_authority_source: <durable locator or none>
publisher_identity: <attributable identity>
publication_authority_source: <source authorizing publication>
published_at: <timestamp or durable event time>
```

## Interpretation

- `plan_ref` is the accepted planning snapshot named by this publication; the carrier commit is not automatically the PlanRef.
- After the first publication, this carrier's Git parent MUST equal `prior_publication_commit`.
- `prior_publication_id` and `prior_plan_ref` MUST equal the validated predecessor carrier's values.
- The publication ref MUST advance non-force from the exact predecessor carrier. A pre-write check without conditional ref advancement is insufficient.
- Transition validation uses the predecessor accepted PlanRef's governance rules. Candidate changes to publication/governance rules become eligible only for later transitions after the candidate is accepted.
- `approval_basis=founding` is valid only for first root publication; `approval_basis=parent` only for authorized child bootstrap.
- Fields that do not apply use `none`.

Cold validation and recovery MUST use the actual configured publication-ref carrier history under `planning/PUBLICATION_TRANSITIONS.md`, not this record's self-reported predecessor fields alone.

Replaying old CURRENT contents at a later carrier does not restore old state. Reversion requires a new authorized transition from the actual incumbent carrier.
