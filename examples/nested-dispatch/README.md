# Inherited child-dispatch walkthroughs

These are fictional source/protocol cases for `planning/NESTING.md`, not live dispatches, authority grants or publication experiments. P0/P1/P2, C1 and G1 abbreviate distinct exact retained PlanRefs; E-P1 and similar names abbreviate their validated committed publication events. Real packages record full SHAs, exact evidence locators and independently verified identities.

## Fixture identity and boundary chain

All repository IDs below are illustrative. Each native plan explicitly adopts compatible `plan-grammar-v2`, `qualified-reference-v1` and the indicated Decision/DATA contracts through accepted publication. Local IDs remain human-chosen. The table supplies complete plan resolver components; an object adds its exact kind and local ID.

| Alias | Repository scheme | Authority | Repository ID | PlanID |
|---|---|---|---|---|
| PARENT | github-repository-id-v1 | github.com | 3001 | PARENT |
| CHILD | github-repository-id-v1 | github.com | 3001 | CHILD |
| GRAND | github-repository-id-v1 | github.com | 3002 | GRAND |

For example, the durable cross-plan reference to PARENT/B is:

```text
repository_identity: {scheme: github-repository-id-v1, authority: github.com, id: "3001"}
plan_id: PARENT
object_kind: milestone
object_id: B
```

PARENT has `A --> B`. CHILD implements B under parent-owned contract K-B and has first Milestone C0 with no local prerequisite. PARENT/B and CHILD/C0 have existing delivery/acceptance authority and contracts; none of the examples creates that authority. CHILD's accepted C1 pins the accepted relationship P1 containing K-B. K-B cites prior authority baseline P0. A later current P2 can change prerequisite readiness while leaving the K-B relationship and C1 pin unchanged. Current-state checks use P2, not P0 or a convenient old P1.

In the multi-ancestor variant, PARENT itself implements GRAND/G-B under K-G; its accepted parent pin is G1. GRAND has `G-A --> G-B`. GRAND is the verified root. This chain crosses one same-repository PlanID boundary and one repository boundary. Do not assume the plans share publication state because two share Git storage.

## Immediate parent blocked and open

Unless stated otherwise, CHILD/C0's local checks, identity, compatible relationship and authority are valid. “Open” below means eligible for this bounded dispatch check; it does not issue authority or accept any Milestone.

| Current accepted parent / observation | C0 substantive dispatch | Reason |
|---|---|---|
| P1 projects A PENDING; B PENDING | Blocked | A is B's unsatisfied hard prerequisite, inherited by C0 despite C0 having no local predecessor. |
| A has an external acceptance receipt, but current P1 still projects it PENDING | Blocked | Evidence/acceptance alone does not create the operative DONE projection and index. |
| Current P2 projects A DONE and indexes valid acceptance; B remains PENDING | Open if all other applicable checks pass | A now satisfies the prerequisite. B itself need not be DONE before its child executes. The unchanged P1 relationship pin need not churn. |
| A is marked DONE but its acceptance index/evidence is invalid | Blocked | A label cannot open the prerequisite. |
| Child locally marks C0 INPROGRESS while A is still unsatisfied | Blocked for new/resumed substantive dispatch | Child projection cannot overrule parent constraints or retroactively authorize the start. |
| Only an unsatisfied dotted `preferred before` edge points to B | No hard block from that edge | Scheduling preference retains its original meaning. |
| A separate hard Gate prerequisite of B has a false objective predicate | Blocked even with A DONE | Every applicable hard prerequisite remains necessary; a deciding Role cannot declare a Gate true by judgment. |
| A hard DATA prerequisite indexes an exact resolution, but its artifact is missing or for the wrong required input revision | Blocked even with A DONE | Current index selection alone does not establish objective usability for this use. |

For the open P2 case the package retains C1/E-C1, qualified PARENT/B and contract K-B, relationship pin P1, current P2/E-P2, the compatibility basis and exact A acceptance/projection evidence. It records why the relevant K-B relationship remains valid. P0's authority-baseline role is not confused with P2's current-readiness role. No parent copy of C0 is needed.

## A higher ancestor remains controlling

Use the multi-ancestor variant with current P2 satisfying A and CHILD/C0 locally open.

| GRAND boundary / chain evidence | C0 substantive dispatch | Reason |
|---|---|---|
| Current G1 projects G-A PENDING | Blocked | The immediate parent is open, but PARENT is implementing blocked GRAND/G-B. |
| Current G2 projects G-A DONE with valid acceptance; K-G remains applicable | Open if all other checks pass | Both inherited boundaries are open. Retain current G2 evidence separately from the G1 pin and P2/C1 evidence. |
| Only old G2 is readable; latest required journal/current evidence is unavailable | Blocked | A historical open snapshot cannot establish current permission. |
| Current G3 reopens G-A while CHILD still pins P1 and PARENT still pins G1 | Blocked for dependent new/resumed dispatch | Current ancestor constraints control even though the relationship pins are unchanged. Reconcile active work under the existing propagation rules. |
| PARENT claims root despite a contradictory accepted K-G child relationship | Blocked | Missing or contradictory ancestry cannot truncate the check. |
| A repeated qualified plan reveals a parent/delegation cycle | Blocked | A cycle is not a completed walk to an accepted root. |

The readiness record includes both boundary rows. Adding a fourth level repeats the same check; no fixed depth limit or parent mirroring of internal child milestones is introduced.

## Selected Decision branches and replacement

In a separate GRAND variant, replace `G-A --> G-B` with Decision D selecting tokens `build` or `defer`, cardinality `exactly_one`. D's accepted definition maps `build` to G-B and `defer` to G-ALT. Each branch can have its own child; all other prerequisites in this table pass. D uses `decision-result-v1`; its deciding Role, inputs and result authority are valid.

| Current GRAND state | CHILD under G-B | Child under G-ALT | Required interpretation |
|---|---|---|---|
| G1 indexes `active_result: none` | Blocked | Blocked | No operative result selects either ancestor branch. |
| Immutable R-build exists but G1 still indexes none | Blocked | Blocked | Record existence is not activation. |
| G2 validly indexes R-build selecting `build` | Open subject to the full chain | Blocked | Selection of the ancestor path is inherited across PARENT to CHILD. |
| Proposed R-defer exists but G2 still indexes R-build | Same as G2 | Blocked | An unpublished replacement cannot switch branches. |
| G3 validly indexes R-defer, explicitly supersedes/deactivates R-build and records affected old-work disposition | Blocked for new dispatch | Open subject to the full chain | New child work uses the current indexed result. Preserve both immutable results and their original definition/input bindings. |
| G3 expressly continues named previously authorized old-branch work | No new dispatch permission | As above | That bounded continuation is not a reopened `build` branch or permission for additional packages. |
| G4 validly revokes the active result and indexes none | Blocked | Blocked | Revocation does not select a fallback branch. |

If these alternatives rejoin at explicit Gate J with predicate “the currently selected branch's Milestone is operative DONE,” evaluate that predicate for a child implementing the outcome after J. Do not demand both mutually exclusive tokens, count an old unselected branch's DONE as selected, or invent a rejoin from diagram layout. If J also requires DATA evidence, its exact current usable resolution must satisfy that predicate/use. An unspecified governing path or unsupported Decision contract blocks that affected boundary until accepted clarification; these cases do not supply a global graph-satisfiability algorithm.

## Explicit preparation is bounded

Return to the blocked `A --> B` fixture. Existing parent authority explicitly permits an assessment of already available documents while A is pending. The accepted permission names its source, read-only inputs, comparison artifact, authorizing Role, excluded implementation/tool effects and relevant ancestor conditions; if GRAND is also closed, the permission must validly cover that boundary too.

| Proposed action | Result |
|---|---|
| Read the named documents and return the authorized comparison | Allowed within the explicit preparatory permission; A and B remain unsatisfied/unaccepted. |
| Begin implementing B after calling the package `research` | Blocked; the effect is substantive execution of the blocked outcome. |
| Use an available read-only tool without an applicable preparation grant | No exemption; tool access or the label alone does not establish permission. |
| Immediate parent permits preparation but lacks authority to permit it under a closed GRAND constraint | Blocked at GRAND; an issuer cannot waive a higher boundary it does not control. |
| Turn the comparison into a Decision selection or acceptance | Requires the distinct valid substantive authority and existing record/publication process; the preparation grant does not provide it. |

## Opaque portion of an ancestor chain

Suppose CHILD cannot natively interpret PARENT's foreign planning system. Its qualified identity and current accepted relationship still resolve. The explicit accepted parent contract allows a stated bounded child implementation only on accepted readiness evidence from the named, independently authorized parent source. That contract defines exact scope/actions, supporting evidence, currentness/revalidation conditions and required upstream coverage.

| Boundary evidence | Result |
|---|---|
| Foreign screen says “ready,” with no contract-defined accepted evidence | Blocked; no invented native status or branch semantics. |
| Evidence covers the immediate parent but omits its still-applicable GRAND boundary | Blocked; opacity cannot erase the remaining ancestor chain. |
| Accepted evidence binds the exact current parent/contract, child scope/actions and validity checks, and validates applicable upstream constraints to GRAND's root under their accepted semantics | Allowed only for the covered work if all other checks pass; retain the evidence with the package. |
| Previously valid evidence is stale or invalidated by a relevant ancestor change | Blocked pending current revalidation; an old “ready” assertion cannot override the change. |
| Evidence says a required upstream branch remains unselected but grants broad implementation anyway | Blocked; readiness cannot waive the hard constraint. Only separately authorized bounded preparation may be eligible. |
| Repository identity or legacy cross-plan mapping is ambiguous | Blocked; an opaque contract cannot guess which authority-bearing object was intended. |

This evidence carries the boundary's accepted readiness conclusion; it does not reinterpret foreign internals, accept the parent outcome, expand delegation, or require parents to reproduce child roadmaps.

## Validation limits

The tables are bounded counterexamples checked against the canonical source. They establish neither a live scheduler/transport guarantee nor global plan satisfiability. Current evidence, independently accepted authority, exact retained records and project-specific controls remain operational requirements. Adopting the rule is a forward accepted planning change; historical dispatch/acceptance records are not rewritten or backdated.
