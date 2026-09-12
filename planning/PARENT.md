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
parent_repository: <owner/repo>
parent_plan_path: <path to parent PLAN.md>
parent_plan_id: <stable parent PlanID>
parent_plan_ref: <exact accepted parent commit SHA>
parent_milestone: <exact parent MilestoneID implemented by this repository>
parent_contract: <durable path/link to parent-facing contract>
scope_owner_role: <RoleID that owns the child boundary>
```

Do not leave placeholders in an operational child relationship.

## Interpretation rules

- `parent_plan_ref` is the accepted parent planning revision that delegated this child scope.
- The child may change internal implementation planning without updating this file while the parent-facing contract remains unchanged.
- Update this file when the parent boundary changes materially: parent identity, parent MilestoneID, parent contract, delegated scope/authority, or other parent-visible semantics.
- A new parent commit does not automatically invalidate the child. Foreman/child Lead should inspect the intervening parent planning diff and update only if this child boundary is affected.
- A child repository may not change this file to grant itself authority. The corresponding parent record must already authorize the relationship.
- Git repository ownership, forks, submodules, branch relationships, or shared commits are not parent authority.
