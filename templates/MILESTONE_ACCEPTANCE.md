# Milestone acceptance template

Use this record when an authorized acceptance authority concludes that one milestone's stated outcome and acceptance criteria have been satisfied.

This is separate from work completion, review completion, evidence production, the roadmap's status class, and the later act of making the accepted fact operative in the current roadmap.

Issued acceptance records are immutable historical receipts. Do not edit or reinterpret an issued acceptance in place. A correction or replacement creates a new durable acceptance record that references or supersedes the prior one. Later invalidation or revocation is a separate durable decision followed by an accepted plan update; it does not rewrite the old receipt.

```text
acceptance_id: <stable ID>
reference_contract: qualified-reference-v1
repository_identity: {scheme: github-repository-id-v1, authority: <GitHub host>, id: <numeric repository ID>}
plan_id: <PlanID>
contract_plan_ref: <exact accepted pre-acceptance PlanRef containing the milestone contract being judged>
milestone_id: <MilestoneID>
accepted_by_role: <local RoleID or qualified cross-plan role reference>
acceptance_authority_plan_ref: <exact accepted PlanRef for the accepting Role's authority>
acceptance_authority_source: <independently accepted source granting this Role acceptance authority over this milestone/scope>
accepted_at: <time or durable event reference>
supersedes: <prior acceptance record or none>
```

`contract_plan_ref` is deliberately **not** the later PlanRef that may record `MILESTONE_DONE`. It identifies the exact contract revision whose outcome, criteria, and authority references are being judged.

The header fixes the Milestone's repository/plan context. A Role in a different plan is fully qualified under `planning/REFERENCES.md`; its separate `acceptance_authority_plan_ref` is in that Role's plan and is not assumed equal to the subject's `contract_plan_ref`. Qualify any external authority-source object and bind its own exact revision. These references identify objects/revisions, not an additional authority or issuer-provenance mechanism.

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
- downstream milestones are operationally unblocked before the current accepted roadmap projects this acceptance;
- downstream milestones are accepted;
- unrelated safety, release, spending, data, or deployment authority is granted.

## Roadmap projection and operational activation

After this acceptance is durable, a later plan/status update may:

- mark the milestone `MILESTONE_DONE`; and
- populate the milestone's `Acceptance record index` with a locator to this record.

That update creates a **different PlanRef**. Call it the projection PlanRef when the distinction matters.

The projection PlanRef does not become the contract revision accepted by this record. This record continues to bind `contract_plan_ref` exactly. The projection does not re-accept the milestone; it makes the already-accepted fact operative in the current roadmap.

Until an accepted projection PlanRef records the milestone as `MILESTONE_DONE` and indexes this acceptance, downstream hard-prerequisite dispatch must continue to treat the current roadmap as not yet operationally opened by this acceptance. Agents must not bypass the current PlanRef merely because they can see the external acceptance record.

Do not edit this acceptance record merely to point it at the later projection revision. If a later revision materially changes the milestone outcome, acceptance criteria, or authority semantics, it is a new contract revision and requires its own acceptance.

If later evidence shows this acceptance should no longer govern current planning, retain this receipt unchanged. Record a separate revocation/reopening/correction decision under valid authority, then reflect that decision through an accepted plan change. Historical acceptance and current operational status remain separate facts.

A roadmap class change or acceptance-record index entry without a valid prior acceptance record does not create acceptance.
