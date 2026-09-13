# Acceptance issuer and issuance-time authority examples

These are bounded source examples for Issue #11, not live plans, holders, publication events or acceptance receipts. P0/P1/P2/C1 stand for distinct exact Git PlanRefs; E0/E1/E2 stand for valid trusted publication events with retained snapshots/carriers; I1 stands for durable attributable issuance evidence. Replace them with actual exact records in an adopting project. No example derives authority from a placeholder, Git access or this document.

The governing rules are `planning/CONVENTIONS.md` -> **Issuer and authority at issuance**, `planning/ROLES.md` -> **Holder attribution**, and `templates/MILESTONE_ACCEPTANCE.md`. Currentness, retention and cross-plan resolution continue to use `planning/PUBLICATION_TRANSITIONS.md` and `planning/REFERENCES.md`.

## Alice is replaced by Bob without changing the contract

Assume prior accepted governance has adopted the issuer-evidence requirements and defined a durable attribution mechanism. The accepted registry binds exact context references `holder/alice/context-A` and `holder/bob/context-B`, not merely a shared account called `team-bot`. The retained mechanism can attribute each issuance action to the actual context and establish its order relative to publication; a self-authored context string alone would not suffice.

| Order | Accepted state or act | What it establishes |
|---|---|---|
| 0 | E0 makes P0 current: AcceptanceLead is held by Alice/context-A; independent grant G0 allows acceptance of M1. | P0 contains M1's outcome, criteria and authority references. No acceptance exists yet. |
| 1 | Under prior valid authority, E1 makes P1 current: AcceptanceLead is rebound to Bob/context-B; M1 and G0 are unchanged. | Bob can now exercise the same Role/scope. Alice no longer can. The contract being judged may still be P0. |
| 2 | Bob/context-B issues receipt A1 using the evidence below; I1 establishes issuance after E1 while P1 remains current. | A1 is Bob's act under P1, judging the unchanged M1 contract at P0. G0 still applies under the current authority check. |
| 3 | Later E2 makes P2 current, rebinding the Role to Carol and narrowing its future scope. | A1 remains immutable evidence of Bob's historical act; P2 cannot replace its issuer/state fields. Current reliance separately checks contract applicability and any explicit revocation/reopening. |

Illustrative A1 identity/issuance block (the actual receipt also includes the exact accepted evidence, criterion determinations, limitations and normal template fields):

```text
acceptance_id: A1
reference_contract: qualified-reference-v1
repository_identity: {scheme: github-repository-id-v1, authority: github.com, id: "4101"}
plan_id: PROGRAM
milestone_id: M1
contract_plan_ref: <P0>
accepted_by_role: AcceptanceLead
issued_by_holder: holder/bob/context-B
authority_state_ref: <P1>
authority_binding_locator: planning/ROLES.md#AcceptanceLead-row
acceptance_authority_plan_ref: <P1>
acceptance_authority_source: <G0 at its exact P0 locator; scope/continuing validity checked in P1>
issuance_evidence: <retained I1: exact A1 content, context-B attribution, accepted attribution rules, E1/P1 and retained carrier evidence, issuance ordering under those rules>
accepted_at: <actual issuance time/event I1>
supersedes: none
```

`#AcceptanceLead-row` denotes an unambiguous record/row locator under this example's accepted registry convention, not a claim that arbitrary Markdown tables automatically have HTML row anchors. The subject header fixes the local Role's plan context. P0 is the judged contract and retained original grant; P1 is the Role/binding state at issuance; P2 is later authority. No field means all three at once. `acceptance_authority_plan_ref` deliberately repeats P1 as the existing authority-revision field; disagreement with `authority_state_ref` would be invalid.

A1 and I1 can use stable record IDs allocated before the act; the retained issuance evidence must bind A1's exact content and cannot be redirected to different content under the same ID. Neither record must contain the SHA of its own carrier commit or name a future publication event. The later audit establishes I1 before E2 from retained ordering evidence under the accepted mechanism. Issuance does not move the publication ref or itself mark M1 DONE. A separately authorized accepted projection must index the valid receipt and project DONE before a Milestone prerequisite opens.

## Attribution, rebinding and ordering counterexamples

| Case | Required result |
|---|---|
| Bob/context-B issues at step 2, citing P0 as contract and P1 as authority state with matching I1 | Issuer check passes, subject to the actual scope, criteria and evidence checks. Contract and authority SHAs need not match. |
| Alice/context-A issues at step 2 using the same Role, G0 and contract P0 | Reject: Alice no longer occupies the Role. The original grant and unchanged contract do not preserve a former holder's authority. |
| Alice cites historically accepted P0 as `authority_state_ref` while P1 is current | Reject stale authority for this new act. Historical acceptance of P0 does not make it current at issuance. |
| Alice writes `issued_by_holder: holder/bob/context-B` but I1 attributes the action to context-A | Reject the mismatch. A claimed holder string cannot replace attributable action evidence. |
| Only `team-bot`, a timestamp and a commit author are recorded for either Alice or Bob | Cannot distinguish the actors under these example bindings; stop acceptance until actual attribution is established. |
| Another context uses Bob's display name/account but only context-B is bound | Reject: shared account ownership or naming does not transfer the binding. |
| Bob changes a mutable profile/title after issuance, but retained I1 and P1 resolve the original context | Historical attribution remains reconstructible. Do not retarget A1 to the new profile resolution. |
| Receipt points only to today's registry, or P1's binding/attribution evidence is unavailable | Historical authority cannot be verified; stop dependent reliance. Do not reconstruct by guessing today's or P0's holder. |
| Bob is proposed in a candidate P1, but E0/P0 is still the accepted current state | Bob cannot act. Alice may still act only under the real current P0 binding and scope; candidate approval/merge alone does not rebind. |
| Candidate both grants acceptance scope and purports to issue acceptance before publication | Reject candidate-only authority and self-authorization. |
| P1 was checked, then E2/P2 changed the binding before the actual issuance | Revalidate against P2; Bob's earlier check does not authorize a later act. Do not backdate A1. |
| P1 and P2 are both retained but evidence cannot establish whether issuance preceded E2 | Stop the affected acceptance/reliance; two SHAs plus an untrusted timestamp do not establish ordering. |
| Carol is today's holder and was not the issuer of A1 | Preserve Bob/context-B and P1 in A1; audit the act at issuance, not against today's holder. |
| P2 removes acceptance scope after A1 was validly issued | A1's issuance history remains valid. A new receipt needs current scope; any current revocation or material contract change is handled explicitly. |
| A separate authorized reopening/revocation invalidates A1 for current planning | Preserve A1/I1 unchanged, record the later decision, and change the accepted current projection/index under existing rules. |
| A correction is issued as A2 after rebinding | A2 has its own issuer, current authority state and issuance evidence, and references/supersedes A1. Do not copy P1 merely because A1 used it. |
| `acceptance_authority_plan_ref: P0` but `authority_state_ref: P1` in a new receipt | Reject inconsistent Role-state fields. Put original G0/P0 in the separate authority-source reference. |
| Same acceptance ID resolves to two different contents | Reject ambiguous evidence binding; do not pick the convenient version. |

## Parent acceptance of a child's Milestone

Let ROOT be in repository `{scheme: github-repository-id-v1, authority: github.com, id: "4101"}` and CHILD in repository `4102` on the same host/scheme. ROOT's accepted P0 is the authority baseline for relationship K1, P1 contains accepted K1, and current P3 still supports K1 but now binds ROOT/AcceptanceLead to Bob/context-B. CHILD's current C1 pins the accepted relationship P1 and contains Milestone M1, whose parent-facing contract references ROOT's accepting Role. Assume all required delegation/acceptance scope is independently granted and compatible.

| Receipt/check | Exact meaning |
|---|---|
| Subject header | Repository 4102, PlanID CHILD, Milestone M1. `contract_plan_ref: C1` judges the child contract. |
| `accepted_by_role` | `{repository_identity: {scheme: github-repository-id-v1, authority: github.com, id: "4101"}, plan_id: ROOT, object_kind: role, object_id: AcceptanceLead}`. A CHILD-local Role with the same name is different. |
| `authority_state_ref` and `acceptance_authority_plan_ref` | Both P3, in ROOT's publication context; binding locator selects Bob/context-B's accepted ROOT Role row. |
| `issued_by_holder` and `issuance_evidence` | Bob/context-B under ROOT's retained accepted attribution rules; exact receipt content and ROOT's P3 currentness/order at issuance, plus the child/source/relationship evidence actually relied upon. |
| Relationship evidence | K1 at P1, child's pin P1, and current-parent compatibility/authority at P3. P0 authorizes K1's creation but does not contain it; P1 does not identify today's holder by itself. |

| Counterexample | Required result |
|---|---|
| Use C1 as ROOT's authority state because it is the receipt's contract revision | Reject wrong plan/revision context; resolve each plan's own publication evidence. |
| Use ROOT's P1 relationship pin as current authority after P3 rebound the holder | Reject the stale issuance binding, even if the relationship remains otherwise compatible. |
| ROOT's newer current state revoked the relevant scope, but child still pins P1 | Reject the new acceptance; the old pin cannot preserve revoked authority. |
| Same layout uses two plans in one repository instead of two repositories | Still qualify ROOT versus CHILD and resolve each plan's own current state. Shared Git SHA/history does not merge Role identity or publication contexts. |
| Repository alias resolves to a different machine ID, or a cross-plan Role is only a bare `AcceptanceLead` | Reject mismatched/ambiguous reference; issuer evidence does not repair a missing authority identity. |
| Child has not accepted compatible reference semantics and no explicit accepted mapping exists | Stop affected cross-plan acceptance; do not infer a native interpretation from copied fields. |

## Adoption and historical receipts

| Case | Required result |
|---|---|
| Existing project proposes these fields but has not accepted the migration | Existing accepted rules continue. The candidate cannot authorize itself or silently reinterpret old receipts. |
| Accepted migration becomes current; a later acceptance is issued | Record the new issuer/state/evidence fields and accepted attribution basis for that act. No roadmap grammar change is needed. |
| Old receipt lacks issuer context and exact issuance authority evidence | Keep it unchanged and report the audit limit. Do not insert Alice from its old contract or Bob from today's registry. |
| Independently authorized historical audit finds retained evidence proving the old issuer/state | Create a separate exact supplementary record with provenance and limits, without changing the old receipt or inventing authority it lacked. |
| Current reliance requires provenance that neither the receipt nor retained evidence establishes | Stop that reliance and obtain a valid authorized resolution; do not fabricate or retroactively validate the historical issuance. |

These cases check the portable source contract. They do not implement a runtime validator, provide an identity service, prove a live transport's attribution guarantees, or exercise a publication system. Operational projects must establish their accepted attribution/evidence mechanism and verify real records; unavailable evidence fails closed for the affected act or reliance.
