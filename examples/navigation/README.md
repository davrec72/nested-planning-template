# Human navigation examples

These are nonoperational presentation examples under [the navigation convention](../../planning/CONVENTIONS.md#human-navigation). They add no accepted identities, authority, dependencies or evidence. The existing example roadmaps and all their edges/statuses remain unchanged. No Mermaid interaction or browser experiment is needed to follow the visible links.

## Same-repository child

For a project with parent `planning/PLAN.md` and child `planning/plans/LEARNING/PLAN.md`, the parent's existing R2 Milestone record can contain `Child plan: plans/LEARNING/PLAN.md` when that record is in `planning/PLAN.md`. Its adjacent table row is:

```text
| R2 | child plan | [Child plan](plans/LEARNING/PLAN.md) |
```

The child header then uses `parent_plan_navigation_locator: ../../PLAN.md` and immediately above its diagram renders:

```text
↑ [Parent plan](../../PLAN.md)
```

These deployment paths are illustrative, not files instantiated here. Both resolve from the containing roadmap. If the Milestone record is in another directory, adjust the table's relative spelling to reach the same source target. The separate parent/child PlanIDs, qualified references and relationship/publication state remain required even within one repository.

For a working co-located navigation pair in this source tree, open the [robot roadmap](../robot-plan/PLAN.md#navigation), follow R2 to the [child roadmap](../child-project/PLAN.md), then follow its parent link back. Those pages illustrate fictional external authority identities; their local links only navigate the example copies, not a new authority relationship.

## External child

For the fictional `example-owner/learning-project` deployment described by the robot example, use the child's specific file URL, not the repository landing page. This entire snippet is an **unresolved nonoperational placeholder**, not a claim that the external repository/file exists:

```text
MilestoneID: R2
Child plan: https://<host>/<owner>/<child-repository>/blob/<navigation-ref>/planning/PLAN.md

| R2 | child plan | [Child plan](https://<host>/<owner>/<child-repository>/blob/<navigation-ref>/planning/PLAN.md) |
```

Fill the source with the actual file locator before rendering a working link and derive the row from it. A mutable navigation ref is only for browsing; resolve the child's qualified identity and exact accepted PlanRef/publication evidence independently before any dependent action. An external child can similarly set its parent navigation locator to the parent's specific roadmap URL while retaining its existing relationship pin and contract locator.

## Decision and DATA details

The [node-lifecycle roadmap](../node-lifecycle/README.md#navigation) has visible D0 and REPORT links derived from its illustrative definition index. D0 goes to the section defining its question, outcomes and cardinality; REPORT goes to the section defining its artifact/subject/usability requirements. These same-document fragments are real local targets. The links select no Decision result or DATA resolution, and create no second definition target field.

## No-click and mismatch cases

- With all Mermaid interaction unavailable, R2's Markdown row, the child's visible parent link, and D0/REPORT's Markdown rows still provide every declared navigation target. No click directives are needed in these examples.
- If an instantiated renderer adds a safe click, it must resolve to the same target as the corresponding Markdown link. A click to a repository homepage while the table/source points to `planning/PLAN.md` is a mismatch; correct or omit the click. It cannot override the table.
- A renamed/moved human-facing locator can be repaired as presentation maintenance, preserving source/table consistency. If qualified identity, the semantic contract locator or another planning boundary also changes, the existing accepted-change rules still apply; navigation cannot silently retarget authority.
- An unresolved template target is visibly a placeholder. It is not a broken link presented as a real child plan, permission to infer an identity, or a reason to invent an accepted PlanRef.
