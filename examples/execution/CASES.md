# Execution contract walkthroughs

These are fictional protocol fixtures for manually checking `planning/EXECUTION.md`, not an instantiated plan, live dispatch, acceptance, or scheduler experiment. P1/P2/P3 below stand for distinct exact 40-character accepted Git SHAs with validated journal events E1/E2/E3 and retained snapshot/carrier evidence. In a real package, use those exact identities and retrievable records, never these abbreviations.

All operational fixtures use project `example/research`, PlanID `research`, current accepted `transition-action-v1` configuration, its validated/indexed/reconciled adoption baseline with required checks verified, a configured durable inventory, and serialized claims. A `none` configuration would block their dispatch steps even if inventory were empty; see the adoption eligibility cases in `TRANSITION_ACTION_CASES.md`. Schedule IDs and verification receipts below are **assumed fixture evidence**, not claims that tasks were actually created. These walkthroughs assess specified behavior; they do not prove transport reliability or external enforcement.

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

### Prepared/paused P1 package with unrelated P2 current

Use separate variants of `WP-DECISION-1/r1`: one authorized at P1 but not yet dispatched, and one validly paused after starting at P1. E2/P2 changes an unrelated target while leaving this package's definition, inputs, scope and authority valid. For the paused variant, also assume exact cessation evidence and valid disposition/reauthorization of its prior stop within the unchanged package bounds. A P2 change alone is not resume permission.

Before the proposed first dispatch or resume, the durable facts are distinct:

```text
immutable package: WP-DECISION-1/r1; plan_ref=P1; target_record=P1:planning/decisions/D0.md; authorization_id=AUTH-1
attempt/inventory: current_checked_plan_ref_and_publication_event=P2/E2
current_validation_evidence_and_conclusion: exact E1-through-E2 reconciliation plus each check below; permitted only when all pass
```

For both variants, Foreman validates E2/P2 with retained journal/snapshot/carrier evidence; current accepted v1 configuration and indexed/reconciled adoption baseline; all outstanding publication/material actions and verified checks; current Alice/Lead authority and AUTH-1 validity for Bob/B; D0's continued applicability and current prerequisites/operative dependency evidence; exact S1/S2 revisions and permitted use; current serialized fence state; and any revocation or scope/semantic change. Parent bindings are explicitly `none` in this root fixture; a nested variant must validate the complete ancestor chain. Retain each result and why P1's frozen definition remains usable at P2.

| Variant / attempted shortcut | Required outcome |
|---|---|
| Prepared P1/r1; unrelated P2 current; every current check passes | First dispatch may use P1/r1/AUTH-1. Record P2/E2 separately; do not manufacture r2 merely to replace P1 with P2. |
| Validly paused P1/r1; unrelated P2 current; every current check and prior-stop disposition passes | Resume the same authorized attempt under the current serialized guard. Preserve P1/r1 and its evidence; retain the separate P2/E2 check. |
| Foreman writes P2 into r1's `plan_ref` to make it “current” | Reject mutation of the issued package. P1 identifies the authorization/target baseline; P2/E2 belongs in current validation. |
| D0's file is unchanged, but Lead was rebound or AUTH-1 expired/revoked | Block affected execution pending current authorized revalidation/reissue. Unchanged target text and historical P1 authority do not establish current permission. |
| Current target meaning, permitted inputs/scope, required authority, executor grant or reserved decisions materially differ | Suspend/revalidate and obtain the required new authorized package revision; never relabel the difference “unrelated.” |
| Current prerequisite closes, a governing Decision branch is unselected, DATA is unusable, or an ancestor boundary is closed | Block dependent work despite P1's open definition; use current C/B1/B2 evidence, not the historical package baseline as readiness. |
| Current v1 adoption/baseline is invalid, reconciliation/checks fail, or a material stop remains unresolved | Block the affected dispatch/resume. Recording P2/E2 does not prove eligibility or application. |
| A publication fence intervenes after the current-state check | The existing serialized guard blocks the affected dispatch/start/resume; a saved P2 check cannot bypass that fence. |
| P2 is only a candidate, or its required journal/retention evidence is unavailable | Do not treat candidate P2 as accepted current state. Follow existing fail-closed publication validation/recovery; the frozen P1 package does not repair missing evidence. |

## 3. A dropped pause is outstanding work

Use a separate long-running test package `WP-TEST/r1`, attempt `T1`, at P1/E1. The package allows bounded five-minute segments and an explicit safe-stop procedure. In the fixture, Foreman's publication reconciliation runs every two minutes, acknowledgement timeout is one minute, and application timeout is two minutes. These values illustrate configured finite policy, not universal defaults.

The obligated recipient is Tester/context T. Receipt alias `Q2-T1` binds the full key `Q2 + Tester/context T + WP-TEST/r1/T1` within this fixture's project/plan. Direct and fallback routes below reach that same recipient/context; they are retained transport attempts inside Q2-T1, not separate receipts.

This fixture assumes explicit `transition-action-v1` adoption and a valid predecessor-approved TA2 manifest retained in E2's carrier, bound by its journal path/blob/record ID. TA2 contains the exact inventory baseline, Q2/T1/recipient/action/route payload, acknowledgement due at 12:03, application due two minutes after the exact acknowledgement, and S-ACK/S-APPLY logical recovery obligations. Thus the 12:02 reconciler can reconstruct the missing request without the lost wake. See `examples/execution/TRANSITION_ACTION_CASES.md` for the full manifest, approval/retention order, legacy and partial-replay cases.

| Time (UTC) / event | Durable state and required behavior |
|---|---|
| 12:00: E2/P2 validly publishes a scope reduction with `pause`; initial Foreman wake is lost | P2 is current. E2 remains after the inventory's E1 reconciliation marker, so the scheduled reconciliation can discover it. No claim that T1 stopped. |
| 12:02: verified publication check reads E2 | It indexes request Q2/receipt Q2-T1, exact package/revision/attempt, recipient and transport route, and real recovery checks S-ACK/S-APPLY. Only then may the reconciliation marker advance to E2. T1 is `pause-requested`; last applied event is still E1. |
| 12:02: direct-send route rejects an archived target | Record `sent/wake attempted`, `rejected`, delivered unknown/not established, no acknowledgement or application. Keep **not confirmed stopped**. No automatic unarchive authority. |
| 12:03: S-ACK fires | Query the supported fallback and actual effects, attempt an authorized wake, and escalate if still unreachable. Do not dispatch a replacement or report `paused`. Maintain a verified next check for unresolved work. |
| 12:04: worker responds through fallback | Exact Q2-T1 acknowledgement from Tester/context T satisfies acknowledgement in the same receipt; retain the failed direct attempt. It reports a tool still draining, so state remains `pause-requested`; acknowledgement is not application. S-APPLY remains necessary. |
| 12:05: worker's bounded checkpoint cannot validate continued scope | It starts no further segment and uses its authorized safe stop. A non-interruptible/unbounded job would not have been eligible under this package. |
| 12:06: applied receipt proves last action, retained output, and every tool stopped | Foreman records `paused`, last applied event E2, exact evidence and disposition of S-ACK/S-APPLY, then closes the reconciled Q2-T1 obligation. The rejected direct route remains history, not another open receipt. Only the proved stopped scope is confirmed. |

If no applied receipt/enforcement proof arrives at 12:06, the application timeout escalates; T1 remains **not confirmed stopped**. A timestamp, timeout, missing target, or cancelled schedule cannot substitute for cessation evidence. An unenforced lease cannot justify a competing T2. Sensitive work requiring faster stop guarantees needs the project's explicit enforceable lease/fencing policy before dispatch.

| Ordering counterexample | Required outcome |
|---|---|
| E2 arrives twice after application | Preserve duplicate evidence; do not apply the pause twice. |
| E3 validly changes future scope but an old E2 message arrives later | Reconcile journal order; the old message cannot undo E3's valid applied disposition. |
| E3 says `continue` while Q2's stop is unresolved | Do not close Q2 on that word. Reconcile E2/E3 and explicit stop disposition; get valid reauthorization before resuming. |
| Only Foreman acknowledges E2; an independently obligated child coordinator never acknowledges Q2 | That coordinator's own recipient/attempt receipt stays outstanding. Parent receipt does not prove child cessation. |

| Receipt-key counterexample | Required outcome |
|---|---|
| Retry, webhook or prompt reaches the same Tester/context T for Q2 and WP-TEST/r1/T1 | Append transport observations to Q2-T1; do not create another receipt or overwrite earlier route failures. |
| Fallback reaches a different obligated recipient/context | Use a separate receipt for that recipient; it does not automatically acknowledge/apply or close Tester's Q2-T1 obligation. |
| The same recipient has a different independently authorized package revision/attempt | Its receipt has a different key. Merely creating a receipt cannot authorize that work attempt. |
| A new request Q3 concerns the same recipient and package attempt | Q3 has its own receipt; Q2 remains until reconciled or explicitly validly superseded, with history retained. |
| A nested coordinator must itself acknowledge/apply Q2 | Give that obligated coordinator its own receipt; the worker's receipt cannot discharge it. |
| A relay only forwards Q2 to Tester/context T | Record the transit route/observation inside Q2-T1; forwarding alone does not create a new obligated recipient or receipt. |

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

### Fixed inventory identity and permitted succession

These independent variants use an operationally adopted inventory A, logical conditional-serialization mechanism/domain A and its accepted history contract. At P1, A retains running T1, open pause receipt Q, live check S, the current holder/claim, reconciliation/application markers and an active/uncertain publication fence. The fixture assumes exact accepted configuration and supporting authority/evidence; these labels are not live stores or experiments.

| Proposed change / observation | Required result |
|---|---|
| P2 switches current discovery to inventory B/mechanism B under the same execution-contract version | Reject before publication/ref movement. A predecessor-side manifest/fence cannot make B a valid successor store or hide T1/Q/S/the claim/markers/fence. |
| B copies similar or even apparently complete rows from A | Still reject same-version identity/mechanism migration. Ad hoc copies do not establish a versioned handover or preserve the same conditional domain. |
| Locator is unchanged, but P2 changes serialization mechanism, coordination domain or required history semantics | Reject before ref movement. Matching the locator string alone does not preserve the fixed contract. |
| Foreman F1 is replaced by currently authorized F2 while remaining on A | F2 validates/reconstructs A and obtains a new serialized claim with prior-claim disposition. Retain T1/Q/S and fence history; no duplicate dispatch, lost receipt or implicit fence release. Holder succession is not inventory migration. |
| Authorized writer credential/session/route rotates inside A | Allowed only when current writer authority and the same underlying mechanism/domain/history remain valid, with retained old/new identity/route and change evidence. Credentials do not authorize a new store or bypass the current claim. |
| S is replaced by S2 inside A | Follow existing scheduler reconciliation: verify actual state, retain old/new IDs and disposition, verify S2 and reconcile possible duplicate wakes. No live-check assumption or state loss. |
| A is unavailable or its identity/mechanism evidence is contradictory | Fail closed for dependent managed execution; do not initialize B, guess A's obligations empty or clear its uncertain fence. Preserve recovery/escalation obligations. |
| First operational adoption chooses initial A | Prior/root/parent authority may establish A's initial locator/identity/mechanism/domain/history contract, with complete legacy/adoption baseline. Dispatch waits for accepted adoption, all carried records indexed/reconciled and verified checks. No historical state is fabricated. |
| Provider upgrades its implementation within A | Permitted only with evidence of the same accepted logical conditional-serialization/history contract and domain. A changed store/domain is not an upgrade exception. Ordinary revisions and package/receipt/result/check/fence lifecycles remain mutable. |

This is no inventory/provider migration framework. A future identity/mechanism move requires a separately specified/versioned contract. The fixed domain is distinct from each runtime fence's affected scope and from the current holder/claim.

### Other adoption and node cases

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
