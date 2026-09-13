# Root founding record

Use this template only for a **root project** with no accepted parent authority.

Instantiate as `planning/FOUNDING.md` before first publication.

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
publication_journal_kind: <append-only/tamper-evident mechanism>
publication_journal_locator: <cold-reader locator>
publication_journal_trust_basis: <why committed events are durable/non-rewritable or detectably invalid>
plan_snapshot_retention_kind: <protected immutable ref | permanent archive | equivalent>
plan_snapshot_retention_locator_or_pattern: <cold-reader locator/pattern>
plan_snapshot_retention_trust_basis: <why historical published PlanRefs remain fetchable or deletion is detectable>
carrier_evidence_retention_kind: <immutable Git/object archive | equivalent>
carrier_evidence_retention_locator_or_pattern: <cold-reader locator/pattern>
carrier_evidence_retention_trust_basis: <why accepted carriers and validation-critical Git objects remain fetchable or deletion is detectable>
continuing_external_authority: none
```

## Rules

- The Founding Authority exists outside the Role ontology solely to solve the first-authority bootstrap problem.
- Repository ownership/write access, seniority, tool access, or this file do not by themselves make someone the Founding Authority.
- The founding scope is bounded to establishing the first accepted planning/authority/governance state and its initial publication trust contract.
- The Founding Authority approves the exact first candidate plus the exact initial publication ref, trusted journal contract, PlanRef-retention contract, and carrier-evidence retention contract.
- Bare Git ancestry or a local reflog alone is not a conforming trusted publication journal for cold reconstruction.
- First publication must retain the exact candidate independently of ordinary branches before its journal event commits.
- First publication must also retain the exact first publication carrier, its tree/CURRENT, and required parent evidence before its journal event commits.
- Every later accepted carrier must remain cold-fetchable for at least the publication-journal lifetime, including displaced accepted carriers after divergent recovery.
- Recovery must retain the quarantined invalid suffix evidence required by `planning/PUBLICATION_TRANSITIONS.md`; a live-ref path alone is not sufficient durable evidence.
- After the first valid trusted publication-journal event, the founding exception expires.
- Any continuing authority of the founder must appear as an ordinary Role/binding in the first accepted Role registry.
- Do not reuse the founding record as later plan-change authority.
- Do not silently change the publication ref, journal trust source, PlanRef retention, or carrier-evidence retention mechanism after bootstrap. A later change requires an explicit authorized migration under already-current governance.
- Preserve the original founding record as history.

If the repository is a child of an accepted parent plan, use accepted parent authority rather than inventing a root founder. That parent authority must explicitly cover the child's initial publication ref/journal/PlanRef-retention/carrier-retention contract as well as its scope and authority state.
