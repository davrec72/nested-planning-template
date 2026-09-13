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
issued_by_holder: <durable attributable holder/actual context reference, matching the accepted binding>
authority_state_ref: <exact accepting Role plan PlanRef current at issuance>
authority_binding_locator: <exact Role definition/holder-binding path and record at authority_state_ref>
acceptance_authority_plan_ref: <same exact PlanRef as authority_state_ref>
acceptance_authority_source: <independently accepted source granting this Role acceptance authority over this milestone/scope>
issuance_evidence: <retained attributable event/evidence binding exact receipt, issuer and accepted authority/publication state and order at issuance>
accepted_at: <time or durable event reference>
supersedes: <prior acceptance record or none>
```

`contract_plan_ref` is deliberately **not** the later PlanRef that may record `MILESTONE_DONE`. It identifies the exact contract revision whose outcome, criteria, and authority references are being judged.

The header fixes the Milestone's repository/plan context. A Role in a different plan is fully qualified under `planning/REFERENCES.md`; `authority_state_ref` and the matching `acceptance_authority_plan_ref` are in that Role's plan and are not assumed equal to the subject's `contract_plan_ref`. Qualify any external authority-source object and bind its own exact revision. Qualified references identify objects/revisions; they do not themselves attribute an issuer or grant authority.

The milestone contract may name `accepted_by_role` and an authority-source locator, but those fields do not grant authority. Before issuing this record, verify that the cited authority source is independently accepted and actually covers this milestone/scope. If not, do not issue acceptance.

## Issuance authority evidence

Follow `planning/CONVENTIONS.md` -> **Issuer and authority at issuance** and `planning/ROLES.md` -> **Holder attribution**. Record or exactly link:

- the accepted attribution rules and evidence identifying the actual issuing holder/context, including disambiguation when several contexts share an account;
- the exact Role definition and holder binding at `authority_state_ref`, with the trusted publication event and retained snapshot/carrier evidence establishing the state current at issuance;
- the independently accepted acceptance grant and each external authority/relationship revision checked at issuance, with its own publication evidence;
- the attributable issuance action/event binding the exact receipt content, issuer and issuance order under those rules. An earlier current-state check alone does not prove authority remained current when the act occurred.

Do not substitute the holder at `contract_plan_ref` or today's holder for `issued_by_holder`. If the actual issuer, binding, authority scope or ordering cannot be verified, do not issue acceptance. Preserve the receipt and linked evidence for historical audit; later holder/scope changes do not rewrite them. This template supplies no signature or identity-provider infrastructure.

For an existing project, adopt these requirements by an accepted planning change before subsequent issuance. Do not backfill an old receipt in place; record any demonstrable supplemental historical evidence separately, with its limitations, under the canonical migration rules.

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
