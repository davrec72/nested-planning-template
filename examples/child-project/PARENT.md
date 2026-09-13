# Example child-side parent relationship

The repository IDs 1001/1002 and readable names are fictional examples, not verified live bindings. Operational adoption requires accepted publication and verified provider identities under `planning/REFERENCES.md`.

```text
mode: child
reference_contract: qualified-reference-v1
child_plan: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1002"}, "plan_id": "LEARNING", "object_kind": "plan"}
parent_plan: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}, "plan_id": "ROBOT", "object_kind": "plan"}
parent_repository_locator: example-owner/robot-plan
parent_plan_path: planning/PLAN.md
parent_plan_ref: <P1: exact accepted parent relationship SHA containing the contract>
parent_milestone: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}, "plan_id": "ROBOT", "object_kind": "milestone", "object_id": "R2"}
parent_contract: {"repository_identity": {"scheme": "github-repository-id-v1", "authority": "github.com", "id": "1001"}, "plan_id": "ROBOT", "object_kind": "contract", "object_id": "ROBOT-R2-LEARNING-v1"}
parent_contract_locator: examples/robot-plan/PARENT_CONTRACT.md
scope_owner_role: LearningLead
```

P1 contains the parent contract whose `authority_baseline_plan_ref` is P0. This child pin deliberately names P1, not P0. A later accepted child snapshot C1 contains this pin; it does not insert C1 into its own content. Current parent state may later be P2 while this valid P1 pin remains unchanged for an unaffected relationship. All abbreviations here must be replaced with verified exact accepted identities in an operational project.

The child may reorganize its internal learning roadmap while this parent-facing contract remains unchanged.

The child must escalate before changing the parent-facing outcome, acceptance criteria, delegated authority, parent-level dependency meaning, or any parent-owned contract.
