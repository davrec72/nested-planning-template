# Parent plan relationship

Set exactly one mode.

## Mode

```text
mode: root
```

Use `root` when this repository is not currently delegated as a child of another plan.

If this repository is a child of another plan, replace the mode and fill every field below:

```text
mode: child
reference_contract: qualified-reference-v1
child_plan: <qualified child plan reference; fixes local scope_owner_role context>
parent_plan: <qualified parent plan reference>
parent_repository_locator: <readable owner/repo or URL>
parent_plan_path: <path to parent PLAN.md>
parent_plan_ref: <exact accepted parent relationship PlanRef containing the bound contract/delegation>
parent_milestone: <qualified parent milestone reference implemented by this child>
parent_contract: <qualified parent contract reference>
parent_contract_locator: <durable path/link at parent_plan_ref>
scope_owner_role: <RoleID that owns the child boundary>
```

Do not leave placeholders in an operational child relationship.

Use the full qualified tuples from `REFERENCES.md`. Readable names/paths only locate those objects. This header is for an explicitly adopted `qualified-reference-v1` boundary; do not silently reinterpret legacy bare IDs.

## Interpretation rules

- `parent_plan_ref` is the child's pin to the accepted parent relationship revision containing the bound contract/delegation. The parent-side contract instead cites its prior `authority_baseline_plan_ref`; the two SHAs normally differ at creation. Neither record needs its own containing SHA. See `REFERENCES.md`.
- The child may change internal implementation planning without updating this file while the parent-facing contract remains unchanged.
- Update this file when the parent boundary changes materially: parent identity, parent MilestoneID, parent contract, delegated scope/authority, or other parent-visible semantics.
- A new parent commit does not automatically invalidate the child. Foreman/child Lead should inspect the intervening parent planning diff and update only if this child boundary is affected.
- Resolve the current parent PlanRef from its trusted journal before dependent use and verify that the pinned relationship/authority still applies. A historical pin is not a bypass around current scope/revocation. Unrelated parent snapshots may carry the same relationship without requiring the child to repin.
- For substantive child dispatch/resumption, also resolve every applicable ancestor prerequisite and selected Decision-branch constraint under `NESTING.md`. The relationship pin alone does not prove readiness; retain current boundary checks or the explicit accepted opaque-boundary readiness evidence required there.
- A child repository may not change this file to grant itself authority. The corresponding parent record must already authorize the relationship.
- Git repository ownership, forks, submodules, branch relationships, or shared commits are not parent authority.
