# Dependency satisfiability examples

These are manual source fixtures for Issue #16, not operational plans or runtime tests. Use `planning/SATISFIABILITY.md` with the existing conventions/node/publication/execution contracts. Local IDs have one fixed example plan context. P0/P1/P2 denote exact distinct accepted PlanRefs and their trusted events in an instantiated project; the abbreviations are not live authority. Assignment, independent authority, operational adoption and ancestor readiness are assumed valid only where stated, and still need actual validation before dispatch.

## Mutual deadlock and self-dependency

M1 and M2 are PENDING with valid contracts, one assigned Role each, no acceptance awaiting projection and no independent transition or existing execution that can supply an output. Their only dependencies are:

```text
M1 --> M2
M2 --> M1
```

There are no actual seeds. M1 cannot be marked attainable before M2; M2 cannot be marked before M1. The first pass adds nothing. The residual set {M1, M2} has no route without one of its own members: **blocked-cycle**, neither may start. Adding an unrelated predecessor-free M3 makes M3 attainable but does not repair this component. Valid assignments or an INPROGRESS class edit do not supply missing evidence.

For `M1 --> M1`, reject the self-dependency immediately, even if a copied DONE class makes it look satisfied. No topological ordering or acceptance claim legitimizes that definition. `G --> G` and `D -- "A" --> D` are likewise invalid self-prerequisites; authority edges are a different relation.

If M1 instead already has a valid immutable acceptance awaiting an authorized DONE/index projection, that is a different starting state. An explicit witness may project M1, then execute M2: its required evidence and transition exist outside the circular wait. M2 still cannot dispatch before the projection actually becomes current. The checker must not confuse this evidenced transition with assuming M1 will somehow finish while M2 blocks its start.

## OR escape and N-of-M threshold

X and Y are PENDING, have no predecessors, and can be independently executed under valid authority. M is PENDING. All outcome production still requires actual successful work, acceptance and accepted DONE projection. Consider:

```text
X --> G
M --> G
G --> M
```

G's exact predicate is “at least one of X and M is currently DONE with valid indexed acceptance.” The picture contains M -> G -> M, but G can use X instead of M.

| Pass | Feasibility marks and justification | Actual readiness in initial P0 |
|---|---|---|
| 0 | No DONE seed | G false; M blocked. |
| 1 | X attainable: no predecessors; record hypothetical delivery, valid acceptance and later projection | X alone may start, subject to all independent checks. |
| 2 | G attainable using sufficient set {X} | A hypothetical X mark does not make G true now. |
| 3 | M attainable using G | M waits for the real X DONE/index projection and a current true G check. |

After the real projection in P1, G is true from X and M may dispatch with current checks. This is **feasible-but-waiting** initially, not a blanket cycle rejection and not permission to start M at P0.

For a threshold variant, add `Y --> G` and define G as “at least 2 of the distinct inputs X, Y, M are currently DONE with valid indexed acceptance.” Pass 1 marks X and Y; pass 2 marks G using {X, Y}; pass 3 marks M. One independent input is insufficient: if Y instead requires M, only X marks, and {Y, G, M} remains blocked-cycle. Counting X twice cannot satisfy 2-of-3. Changing the predicate to AND also removes the escape because M is then indispensable.

## Only the operative Decision selection participates

D adopts `decision-result-v1` with `selection_cardinality: exactly_one`, tokens A/B and a valid immutable selection R_A indexed by current P1. The explicit outcome mappings put MA on A and MB/MC on B. D's own prerequisites/inputs are satisfied. The graph fragment is:

```text
D -- "A" --> MA
D -- "B" --> MB
MB --> MC
MC --> MB
MA --> G
MB --> G
G --> Z
```

MA, MB, MC and Z are PENDING. G's precise predicate is “at least one branch Milestone, among MA for A and MB for B, whose token is selected by D's current indexed result is currently DONE with valid indexed acceptance.” This is an explicit OR rejoin. Assignment/`decides` edges are omitted from this dependency-only fragment, not from the required authority records.

| State or attempted interpretation | Walkthrough and required conclusion |
|---|---|
| Current P1 indexes R_A | A guard is open; MA is attainable, then G using {MA}, then Z. Their current scope is feasible. MB/MC remain deferred on unselected B; they are not required just because drawn. Their cycle is retained as a blocker to future B activation. |
| Delete the closed B edge and call MB a free starting node | Invalid: the B guard remains false. MB is also mutually dependent with MC. Neither may dispatch. |
| MA is attainable but not actually DONE | G is still false and Z cannot start. Only the actual later DONE/index plus current G evidence opens Z. |
| D has `active_result: none` | Neither A nor B opens; downstream scope waits for a valid accepted selection. Authorized D research can be feasible against D's own prerequisites; it does not choose A. |
| R_B exists but is not indexed | P1/R_A still governs. The record alone cannot activate B. |
| Candidate P2 explicitly replaces R_A with R_B under normal authority/history/work-disposition rules | Analyze B as a candidate scenario: MB requires MC, MC requires MB, and no seed exists. Reject a claim that B is dispatchable. An actual accepted selection cannot by itself repair that cycle; dependent execution remains blocked pending an authorized dependency repair. No speculative MA success counts for the selected-only Gate under B. |
| Z instead has ordinary hard inputs from both MA and MB | AND applies. Do not erase MB to make Z feasible under A. The B guard prevents its new execution; without valid satisfying evidence for both required inputs, Z remains blocked. |
| D permits `one_or_more` and currently selects both A and B | Both branch scopes are applicable. A's witness does not prove MB/MC feasible. Diagnose their component; evaluate the rejoin's exact predicate separately. |

Changing a selection needs the existing immutable replacement, old-branch disposition and accepted publication. This example supplies no new activation rule or authority and does not require a parent to mirror child internals.

## Additional adversarial boundaries

| Case | Required result |
|---|---|
| Role R is assigned to M and decides D; authority diagram has a separate relation back to R | Exclude those edges from this dependency analysis. Validate assignment and delegation acyclicity under their own rules; passing dependency analysis cannot repair authority defects. |
| M1 hard-precedes M2, while M2 has a dotted `preferred before` edge to M1 | The preference is not a hard cycle. Witness M1 then M2 remains possible. |
| A required DATA artifact is missing/wrong-revision/withdrawn or its resolution is unindexed | No actual seed. An independent, explicitly described producer/resolution/publication path may support conditional feasibility, but actual use stays blocked until the exact current DATA rules pass. An unexplained external promise is unknown. |
| Gate needs exactly one of X/Y, but the proposed witness has already made both true | The monotone shortcut does not apply. Re-evaluate exact states and reject that witness; a different valid finite sequence needs explicit evidence, or the conclusion is unknown. |
| Two individually possible input observations expire or cannot coexist | Do not union them to satisfy a Gate. Require a state-by-state witness and recheck at actual use. |
| Local target has no predecessors but an ancestor constraint is closed | Local feasibility does not override full ancestor readiness. Apply NESTING; opaque evidence must explicitly cover the boundary and upstream constraints. |
| Existing package was prepared at P0; unrelated P1 is now current | Preserve the immutable P0 package. Revalidate the analysis and all current-sensitive execution predicates at P1, storing the separate current check; no blanket reissue and no stale-baseline exemption. |
| All dependency checks pass but execution mode is `none`, a fence is held, or a required stop remains unresolved | Dispatch stays blocked under existing EXECUTION rules. Feasibility is not operational eligibility or cessation evidence. |

## Later rework and migration

A legitimate sequence may be M1 accepted/projected in P1, then M2 executed and accepted, then an authorized later rework outcome M3 depending on M2. Those are distinct outcomes in a finite order. Alternatively, a later accepted reopening of M1 preserves its old immutable receipt, removes its current operative index and states a valid new starting state, changed dependencies and active-work disposition. Re-run conformance there. It cannot keep a circular wait and assume the word `rework` supplies a start.

Existing plans explicitly adopt the check under prior governance and record current affected components/legacy work. Historical receipts and PlanRefs remain unchanged; missing historical conformance evidence is not fabricated. A candidate analysis that passes neither publishes itself nor makes future states current. An unresolved component can remain explicitly blocked/deferred planning scope, with independent work assessed separately, but cannot be represented as dispatchable.
