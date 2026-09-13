# Execution contract walkthroughs

These are fictional protocol fixtures for manually checking `planning/EXECUTION.md`, not an instantiated plan, live dispatch, acceptance, or scheduler experiment. P1/P2/P3 below stand for distinct exact 40-character accepted Git SHAs with validated journal events E1/E2/E3 and retained snapshot/carrier evidence. In a real package, use those exact identities and retrievable records, never these abbreviations.

All fixtures use project `example/research`, PlanID `research`, a configured durable inventory, and serialized claims. Schedule IDs and verification receipts below are **assumed fixture evidence**, not claims that tasks were actually created. These walkthroughs assess specified behavior; they do not prove transport reliability or external enforcement.

## 1. Standalone Decision research

At P1, D0 asks “Pursue option A or B?” and has no unsatisfied incoming prerequisite. Lead is its one deciding Role. The accepted Lead authority permits commissioning read-only option research; Alice is its current holder. Neither option's downstream implementation Milestone may begin before its own prerequisites are operative. D0 is still a Decision.

The package's relevant exact bindings would be:

```text
work_package_id: WP-DECISION-1
package_revision: r1 (retained immutable fixture record)
project: example/research
plan_id: research
plan_ref: P1 (exact SHA in an operational record)
role: Lead
target_type: decision
target_id: D0
target_record: P1:planning/decisions/D0.md
parent_bindings: none (root fixture)
created_by_role: Foreman
return_to: Lead
return_route: inventory/results/WP-DECISION-1-r1 plus explicit Lead wake
authorization_id: AUTH-1 (Alice-issued exact grant for this revision and Bob context B)
authorization_mode: temporary-executor
authorizing_role: Lead
authorizing_holder: Alice
authorizing_binding_ref: P1:planning/ROLES.md#lead
authority_source: P1:planning/authority/Lead.md#commission-option-research
executor_identity: Bob
executor_context: B
executor_route: supported context-B direct/query route
permitted_actions: read sources S1/S2 at recorded revisions; compare A/B; return evidence
permitted_tools_resources: read-only access to those sources; write only the comparison artifact
reserved_decisions: D0 judgment to Lead; all implementation/acceptance/publication/delegation
valid_from: acknowledgement after E1/authority/prerequisite validation
valid_until: first durable comparison return or 2026-10-01T15:00:00Z, whichever is first
revocation_conditions: Lead stop, expiry, holder rebind/vacancy, changed scope or identity
maximum_execution_segment: five minutes; no action starts if it cannot finish within the bound
checkpoint_policy: validate journal/authority and outstanding requests before each segment
safe_stop_procedure: finish no new reads; preserve partial comparison; report in-flight status
lease_or_fencing_policy: none (bounded cooperative read-only work)
```

Foreman claims attempt `A1`, verifies its return check, and sends this grant. Bob acknowledges `WP-DECISION-1/r1/A1/AUTH-1`, researches, indexes comparison `R1` and explicitly wakes the return route. The inventory becomes `returned`; Lead's separate judgment is still outstanding.

| Proposed action | Contract result |
|---|---|
| Research D0 without any `milestone` field | Permitted after D0's own prerequisites and grant validate. |
| Add a dummy Milestone “Research D0” solely to satisfy the form | Unnecessary and rejected as a form-driven ontology change. |
| Bind the package to the A implementation Milestone and start it before D0 is resolved | Not authorized by the research grant or its prerequisites. |
| Report R1 as D0's final result merely because Bob prefers A | Rejected; only the deciding Role may issue its judgment under current node rules. |

This case tests target selection only. It does not define the Decision-result/branch-activation lifecycle maintained in `CONVENTIONS.md`.

## 2. Executor identity, authority and rebinding

Continue fixture 1 with Lead held by Alice and worker Bob in B.

| Event | Required check and outcome |
|---|---|
| Bob receives `role: Lead` with no AUTH-1 | No temporary authority is inferred; affected execution stops pending a valid grant. |
| Bob validates AUTH-1, current Alice binding and bounded source/action list | Bob can perform the comparison while remaining Bob, not Lead. |
| Bob attempts a write outside the comparison artifact or an unlisted tool | Denied by the action/resource bounds even if credentials permit it. |
| Bob attempts to accept a Milestone, decide D0, bind a Role or delegate to Carol | Denied by this grant; a distinct independently valid Role/authorization path would be required. |
| Foreman proposes enlarging AUTH-1 | Coordination does not grant permission to issue substantive scope; route to the current authorizing Role. |
| E2/P2 rebinds Lead from Alice to Carol | AUTH-1 is suspended; no new segment/resumption until Carol explicitly revalidates/reissues within current authority. |
| E2/P2 changes an unrelated target instead | Reconcile E2, record current validation and why AUTH-1 remains valid; do not restart unchanged work. |
| The Foreman holder changes while Alice/Lead and AUTH-1 remain valid | Recover A1; do not change Bob's identity or issue A2 merely because coordination changed. |

## 3. A dropped pause is outstanding work

Use a separate long-running test package `WP-TEST/r1`, attempt `T1`, at P1/E1. The package allows bounded five-minute segments and an explicit safe-stop procedure. In the fixture, Foreman's publication reconciliation runs every two minutes, acknowledgement timeout is one minute, and application timeout is two minutes. These values illustrate configured finite policy, not universal defaults.

| Time (UTC) / event | Durable state and required behavior |
|---|---|
| 12:00: E2/P2 validly publishes a scope reduction with `pause`; initial Foreman wake is lost | P2 is current. E2 remains after the inventory's E1 reconciliation marker, so the scheduled reconciliation can discover it. No claim that T1 stopped. |
| 12:02: verified publication check reads E2 | It indexes request Q2/receipt Q2-T1, exact package/revision/attempt and route, and real recovery checks S-ACK/S-APPLY. Only then may the reconciliation marker advance to E2. T1 is `pause-requested`; last applied event is still E1. |
| 12:02: direct-send route rejects an archived target | Record `sent/wake attempted`, `rejected`, delivered unknown/not established, no acknowledgement or application. Keep **not confirmed stopped**. No automatic unarchive authority. |
| 12:03: S-ACK fires | Query the supported fallback and actual effects, attempt an authorized wake, and escalate if still unreachable. Do not dispatch a replacement or report `paused`. Maintain a verified next check for unresolved work. |
| 12:04: worker responds through fallback | Exact Q2/T1 acknowledgement establishes receipt. It reports a tool still draining, so state remains `pause-requested`; acknowledgement is not application. S-APPLY remains necessary. |
| 12:05: worker's bounded checkpoint cannot validate continued scope | It starts no further segment and uses its authorized safe stop. A non-interruptible/unbounded job would not have been eligible under this package. |
| 12:06: applied receipt proves last action, retained output, and every tool stopped | Foreman records `paused`, last applied event E2, exact evidence and disposition of S-ACK/S-APPLY. Only the proved stopped scope is confirmed. |

If no applied receipt/enforcement proof arrives at 12:06, the application timeout escalates; T1 remains **not confirmed stopped**. A timestamp, timeout, missing target, or cancelled schedule cannot substitute for cessation evidence. An unenforced lease cannot justify a competing T2. Sensitive work requiring faster stop guarantees needs the project's explicit enforceable lease/fencing policy before dispatch.

| Ordering counterexample | Required outcome |
|---|---|
| E2 arrives twice after application | Preserve duplicate evidence; do not apply the pause twice. |
| E3 validly changes future scope but an old E2 message arrives later | Reconcile journal order; the old message cannot undo E3's valid applied disposition. |
| E3 says `continue` while Q2's stop is unresolved | Do not close Q2 on that word. Reconcile E2/E3 and explicit stop disposition; get valid reauthorization before resuming. |
| Only Foreman acknowledges E2; child coordinator never acknowledges Q2 | The child attempt's receipt stays outstanding. Parent receipt does not prove child cessation. |

## 4. Replacement Foreman recovers without redispatch

At the configured inventory, Foreman F2 finds the following retained fixture records after F1 disappears:

| Inventory item | Retained information |
|---|---|
| Package | `WP-DECISION-1/r1`, exact P1/D0/Lead bindings, AUTH-1 and accepted source, attempt A1. |
| Executor / return | Bob/context B, query route, durable result destination and explicit Lead wake route. |
| Dispatch / result | Serialized claim C1; acknowledged start receipt; durable comparison R1 at exact artifact revision. |
| Publication / receipts | Reconciled E1; A1 applied E1; no unresolved material request. |
| Check | Logical `CHECK-A1-RETURN`; old actual ID S1; owner F1; target F1; trigger/next due/action; historical verification receipt. |

F2 first validates current publication/authority and acquires the current serialized coordination claim with C1's owner disposition. It reads R1, queries B when available, and verifies actual S1 state. Suppose the scheduler proves S1 absent. The check becomes `lost/cancelled`; its still-needed Lead return-routing obligation does not vanish. F2 creates S2 owned by F2 for that obligation, verifies S2, and links S1→S2 as `recreated`. It routes the recovered R1 and follows the existing package to coordination closure. **A1 remains the only execution attempt; no research is redispatched.**

Alternative observations have distinct outcomes:

| Observation | Required action |
|---|---|
| S1 is verified live and reaches a capable current coordinator | Retain it with evidence and current ownership/route; no duplicate schedule is needed. |
| S1 liveness cannot be determined | Mark unknown. Query/recover, or make duplicate wake checks harmless/idempotent before any recreation; never let either wake bypass dispatch reconciliation. |
| B is unreachable but R1 is durable and sufficient | Recover the return; do not rerun just to regain a reachable worker. Account separately for any unknown in-flight effects. |
| B is unreachable and no result exists | Preserve unknown execution, schedule recovery/escalation. Absence of R1 is not proof A1 never started. |
| Initial dispatch of A1 had an ambiguous response | Query the existing attempt; repeat delivery only through a proven deduplicating route. No fresh A2 until non-start/terminal/fenced evidence plus new authorization. |
| A new package revision r2 is proposed while A1/r1 is unknown | The package's single current claim still covers A1. A revision/supersession label does not authorize overlapping replacement execution. |
| Old S1 wakes after S2 was created | Both read the current inventory/claim; the settled result prevents repeated dispatch or duplicated substantive handling. |
| F1 was archived, then restored | Verify actual S1; do not infer its survival or resurrection. |

## 5. Adoption and distinct node semantics

| Input | Migration/compatibility result |
|---|---|
| Legacy `milestone: M1` with valid historical evidence | Preserve history and create explicit typed revision; independently recover current executor grant/attempt before continuing. |
| Both `milestone: M1` and `target_type: decision, target_id: D0` | Conflicting bindings block affected dispatch; do not pick a convenient field. |
| DATA artifact returned from a `data` package | Evidence production only; apply current DATA rules separately. No automatic Milestone-style DONE projection. |
| `plan-maintenance` with no accepted scope or authority | Not dispatchable for an instantiated plan; the type supplies neither. |
| Template source maintenance with an externally authorized issue scope and source SHA | Use that actual maintenance authorization; no invented operational PlanID/Milestone/PlanRef. |
| Existing v1 roadmap or incompatible child grammar | This execution form does not migrate node semantics; preserve historical grammar and use an explicit compatibility decision. |
| Valid publication journal but missing required retained carrier evidence | Existing publication rules still fail closed; an inventory or request cannot repair the authority proof. |

## Bounded dogfooding evidence

These recorded observations informed the failure cases; no new experiment is part of this example or contract change:

- [#13 transport and completion evidence](https://github.com/davrec72/nested-planning-template/issues/13#issuecomment-5649922263): the tested direct send to an archived local target was rejected; bare child completion did not interrupt an active parent during the observed 45-second passive wait, while an earlier explicit child message did. Completion and explicit wake remain separate; this is not a universal transport guarantee.
- [#14 archive/scheduler evidence](https://github.com/davrec72/nested-planning-template/issues/14#issuecomment-5649527950) and [unarchive follow-up](https://github.com/davrec72/nested-planning-template/issues/14#issuecomment-5649921756): archiving the schedule-owning local child removed its observed recurring schedule; unarchiving did not restore it. Readable archived history was not permanent deletion. A view card without a status payload was not schedule-liveness proof.
- [#27 compatibility evidence](https://github.com/davrec72/nested-planning-template/issues/27): ancestor archival did not remove the tested descendant or its schedule, while browser Project/Work deletion had different scope/lifecycle. Do not generalize an archive/delete cascade. Generic worker cleanup cannot authorize deletion of an unrelated multi-context container.

The execution contract uses only the verification/recovery implications. It does not implement #26's Foreman topology policy or #27's lifecycle capability schema/efficiency policy, and does not claim to close those issues.
