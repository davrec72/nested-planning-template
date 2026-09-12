# Milestone acceptance template

Use this record when an authorized acceptance authority concludes that one milestone's stated outcome and acceptance criteria have been satisfied.

This is separate from work completion, review completion, evidence production, and the roadmap's status class.

```text
acceptance_id: <stable ID>
plan_id: <PlanID>
contract_plan_ref: <exact accepted pre-acceptance PlanRef containing the milestone contract being judged>
milestone_id: <MilestoneID>
accepted_by_role: <RoleID>
acceptance_authority_source: <independently accepted source granting this Role acceptance authority over this milestone/scope>
accepted_at: <time or durable event reference>
supersedes: <prior acceptance record or none>
```

`contract_plan_ref` is deliberately **not** the later PlanRef that may record `MILESTONE_DONE`. It identifies the exact contract revision whose outcome, criteria, and authority references are being judged.

The milestone contract may name `accepted_by_role` and an authority-source locator, but those fields do not grant authority. Before issuing this record, verify that the cited authority source is independently accepted and actually covers this milestone/scope. If not, do not issue acceptance.

## Milestone contract being accepted

```text
Outcome:
Acceptance criteria:
Acceptance authority reference:
Acceptance authority source:
```

Quote or link the exact contract from `contract_plan_ref`. Do not silently accept a later or differently worded criterion.

## Accepted evidence

List exact evidence/revisions/measurements/reviews relied upon.

- ...

Evidence existing is not itself acceptance. State why the evidence satisfies each acceptance criterion.

## Criterion-by-criterion determination

| Criterion | Evidence | Determination |
|---|---|---|
| `<criterion>` | `<exact evidence>` | `satisfied` |

Do not omit a required criterion. If a criterion is not satisfied, do not issue an acceptance record.

## Limitations / residuals

Record limits that remain compatible with the milestone's stated criteria. Do not weaken the criteria here.

- ...

## What this acceptance does not establish

Unless separately required by the milestone contract, this record does not imply that:

- every attempted work package succeeded;
- every listed implementation step was necessary;
- the assigned delivery Role also possessed acceptance authority;
- downstream milestones are accepted;
- unrelated safety, release, spending, data, or deployment authority is granted.

## Roadmap projection

After this acceptance is durable, a later plan/status update may:

- mark the milestone `MILESTONE_DONE`; and/or
- populate the milestone's `Acceptance record index` with a locator to this record.

That update creates a **different PlanRef**. Call it the projection PlanRef when the distinction matters.

The projection PlanRef does not become the contract revision accepted by this record. This record continues to bind `contract_plan_ref` exactly.

Do not edit this acceptance record merely to point it at the later projection revision. If a later revision materially changes the milestone outcome, acceptance criteria, or authority semantics, it is a new contract revision and requires its own acceptance.

A roadmap class change or acceptance-record index entry without a valid prior acceptance record does not create acceptance.
