# Root founding record

Use this template only for a **root project** with no accepted parent authority.

Instantiate it as:

```text
planning/FOUNDING.md
```

before the first accepted PlanRef is published.

```text
founding_record_id: <stable unique ID>
project_id: <PlanID or project identity>
repository: <owner/repo or equivalent>
founding_authority_identity: <attributable human/org/external authority>
trust_basis: <direct founding instruction | charter | contract | other explicit external basis>
trust_evidence: <durable locator or exact preserved evidence>
founding_scope: <bounded authority this founding act may establish>
initial_plan_scope: <scope of the first plan being ratified>
initial_role_registry: planning/ROLES.md
initial_role_bindings: <summary or durable locator>
initial_publication_protocol: plan-publication-v1
initial_publication_ref: refs/heads/plan-publications | <explicit alternative locator>
continuing_external_authority: none
```

## Rules

- The Founding Authority exists **outside** the Role ontology solely to solve the first-authority bootstrap problem.
- Repository ownership, write access, seniority, tool access, or the presence of this file do not by themselves make someone the Founding Authority.
- The external trust basis must be explicit and attributable.
- The founding scope must be bounded to establishing the first accepted planning/authority state.
- The Founding Authority must approve the exact first candidate **and** the exact initial publication protocol/ref used to publish it.
- The first publication must identify and approve the exact candidate commit being founded.
- After the first valid publication carrier is established and validated, this founding exception expires.
- Any authority the founder should retain after bootstrap must appear as an ordinary Role/binding in the first accepted Role registry.
- Do not reuse this founding record as authority for later plan changes.
- Do not silently change the configured publication ref after bootstrap. A later locator/protocol change requires an explicit authorized migration under already-current authority.
- Do not rewrite the historical founding act in place after first publication. Later corrections/amendments use ordinary accepted authority and preserve the original record.

If the repository is a child of an accepted parent plan, do not create an independent root founding record merely for convenience. Use the accepted parent contract/delegation as the bootstrap authority under `planning/PUBLICATION.md`; that parent authority must also cover the child's initial publication protocol/locator.
