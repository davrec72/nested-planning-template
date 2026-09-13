# Work package template

Use with `planning/EXECUTION.md`. An issued package revision is immutable; changes require a linked new revision and authorization. This form is for an instantiated plan, not a requirement to invent planning identity for external template-source maintenance.

Before creating execution obligations through a new revision/attempt, rebind or supersession, or dispatching/starting/resuming this package, record current eligibility evidence under `planning/EXECUTION.md` -> **Operational eligibility**: accepted `plan-publication-v1` state; accepted `transition-action-v1` configuration and exact carrier path; valid indexed/reconciled adoption/legacy baseline and verified checks; no reconciliation failure blocking this action. Recheck at use, not merely at package preparation. `none`, an empty inventory or an existing grant cannot enable execution.

## Identity and target

```text
work_package_id: <stable ID within the project/plan>
package_revision: <immutable revision or exact content locator>
supersedes_revision: <prior revision or none>
project: <existing project/repository identity>
reference_contract: qualified-reference-v1
repository_identity: {scheme: github-repository-id-v1, authority: <GitHub host>, id: <numeric repository ID>}
plan_id: <PlanID>
plan_ref: <exact accepted commit SHA at authorization>
role: <RoleID whose authority the package serves>
target_type: milestone | decision | data | plan-maintenance
target_id: <stable local node/scope ID>
target_record: <exact definition at plan_ref>
parent_plan: <qualified parent plan reference or none>
parent_plan_ref: <exact accepted parent relationship pin or none>
parent_bindings: <required identity/PlanRef/Milestone/contract bindings under NESTING.md or none>
created_by_role: <coordinating RoleID; not an authority grant>
return_to: <RoleID with final substantive authority for the target/scope>
return_route: <durable result destination and supported wake route>
inventory_locator: <configured execution inventory>
```

`plan_ref` remains the immutable accepted authorization/target-binding baseline; interpret `target_record` there. Before first dispatch, every resume or other obligation-creating action, record the separate exact current PlanRef/publication event and all current-sensitive validation evidence in the attempt/inventory below. Follow `planning/EXECUTION.md` -> **Package baseline and current validation**. An unrelated later PlanRef permits keeping this revision only if those checks pass; material package-defining changes require the existing suspend/revalidate/new-revision path.

For `decision`, use the Decision's own prerequisites and unique deciding Role. Do not fill a fictional downstream Milestone. A child plan's actual parent Milestone remains a separate boundary binding. For `plan-maintenance`, cite a bounded accepted scope; the type is not a new node or authority exemption. See `planning/EXECUTION.md` for every type and legacy `milestone` migration.

Local IDs inherit this package's repository/PlanID and their field's kind. Every cross-plan Role, target, parent contract or return authority uses a full qualified reference under `planning/REFERENCES.md`. Bind each relied-upon external authority's exact PlanRef separately; the package `plan_ref` names only its own plan. For nested use also resolve the current parent PlanRef and verify the pinned relationship still applies. A locator or shared Role name is not authority.

## Objective

State one bounded outcome.

## In scope

- ...

## Out of scope

- ...

## Required inputs

- exact source/candidate revision(s);
- requirements/contracts;
- permitted tools/data/devices;
- relevant accepted evidence.

Record target prerequisites and current publication/retention/authority validation with exact evidence. Producing research, evidence, or a proposed edit must not imply permission to implement its conclusions.

## Executor authorization

```text
authorization_id: <durable exact grant ID/locator>
authorization_mode: temporary-executor | role-holder
authorizing_role: <RoleID with existing permission to commission these actions>
authorizing_holder: <identity at issue>
authorizing_binding_ref: <exact accepted Role/holder binding>
authority_source: <independently accepted authority covering this scope and execution>
executor_identity: <exact person/agent identity>
executor_context: <exact context ID and execution substrate>
executor_route: <supported direct/query route; fallback if available>
permitted_actions: <exhaustive bounded list>
permitted_tools_resources: <tools, repositories, data, devices and effect limits>
reserved_decisions: <Role-reserved decisions and return authorities>
valid_from: <condition/time>
valid_until: <expiry or explicit completion condition>
revocation_conditions: <conditions and authorized stop issuer/route>
maximum_execution_segment: <finite time/effect bound before revalidation>
checkpoint_policy: <where/how publication, authority and requests are checked>
safe_stop_procedure: <authorized handling of in-flight tools/jobs/effects>
lease_or_fencing_policy: <exact project-required policy or none>
```

A temporary executor validates this grant and its authorizer's current accepted authority; it does not pretend to hold `role` or `authorizing_role`. It cannot accept a Milestone, make reserved Decisions, bind Roles, re-delegate authority, or commission another executor through this grant. Separate Role authority requires the distinct holder check and record. `role-holder` mode still requires the executor's own current accepted binding for the action.

Holder rebinding/vacancy, changed executor identity, material scope/authority change, expiry, or a valid stop suspends affected execution as specified by `planning/EXECUTION.md`. Foreman cannot extend or reissue the grant merely because it coordinates it.

## Nested dispatch evidence

For nested substantive dispatch/resumption, retain the ancestor-readiness check required by `planning/NESTING.md` with the package. Bind each qualified parent Milestone/contract, relationship pin, separately resolved current PlanRef/publication event, compatible prerequisite/Decision-result evidence and conclusion through the full ancestor chain. Record exact accepted opaque-boundary evidence and its validity conditions where applicable. An open local graph does not discharge this check. If this is permitted preparation while a boundary is closed, cite its distinct bounded authorization and excluded substantive effects.

## Required return evidence

- exact revision/identity worked on;
- actions actually performed;
- tests/measurements/reviews actually executed;
- failures/skips/limitations;
- produced artifacts/links;
- unresolved blockers;
- whether parent/plan assumptions changed;
- exact package revision, attempt ID, and authorization ID;
- remaining tools/jobs/effects and stop disposition;
- last checked PlanRef/publication event and applied material request IDs.

Write the result durably and index it in the inventory; use the configured explicit wake route. Bare completion does not guarantee that the recipient was notified.

## Review requirements

State any required independent review, reviewer perspective, model/effort/tool limits, and what counts as independent.

## Attempt and future follow-up

Runtime attempt/schedule/receipt state belongs in the inventory, without rewriting this package grant:

```text
attempt_id: <unique exact executor assignment ID>
dispatch_claim: <serialized durable claim evidence>
current_checked_plan_ref_and_publication_event: <exact current accepted SHA and journal event ID at the action>
current_validation_evidence_and_conclusion: <exact reconciliation/current-sensitive checks and permitted/blocked reasons>
check_ids: <logical checks and actual verified scheduler IDs, owners, triggers>
material_receipt_ids: <outstanding receipt locators or none>
latest_result: <durable exact result locator or none>
```

Foreman records/verifies actual follow-ups before asynchronous dispatch and material-request recovery. A `pending` scheduler ID means the check is not established; do not claim `will check later` without a real mechanism.

## Acceptance boundary

State what this package may establish and what it cannot establish.

Completion of a work package is a report/evidence event, not Milestone acceptance or a Decision result. Even when a returning holder also holds acceptance authority, issue a separate Milestone acceptance record binding the exact criteria and accepted evidence under that Role. Use `templates/MILESTONE_ACCEPTANCE.md`.

Never infer acceptance merely from:

- a worker saying `done`;
- a clean review;
- passing tests outside their stated scope;
- merge of an implementation PR;
- the assigned delivery Role being the same holder as an accepting Role.
