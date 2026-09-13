# Cross-plan reference walkthroughs

These are fictional protocol examples, not an instantiated plan, live authority, or actual publication. P0/P1/C1 and carrier names stand for distinct full exact Git SHAs with the required retained evidence. No lifecycle experiment or repository publication is performed by this document.

## Reused local names resolve uniquely

All following machine IDs and hosting names are illustrative, not claims about actual repositories. Each participating plan has explicitly adopted `qualified-reference-v1` in accepted publication. The table lists the complete resolver components; readable locators are deliberately separate.

| Scheme | Authority | Repository ID | PlanID | Kind | Object ID | Readable locator |
|---|---|---|---|---|---|---|
| github-repository-id-v1 | github.com | 2001 | ROOT | role | ChildLead | example/parent |
| github-repository-id-v1 | github.com | 2001 | LEFT | role | ChildLead | example/parent, planning/plans/LEFT |
| github-repository-id-v1 | github.com | 2001 | RIGHT | role | ChildLead | example/parent, planning/plans/RIGHT |
| github-repository-id-v1 | github.com | 2002 | LEFT | role | ChildLead | example/other-child |
| github-repository-id-v1 | ghes.example | 2001 | LEFT | role | ChildLead | example/child on another host |

These five Roles have five different qualified identities despite sharing `ChildLead`. LEFT and RIGHT may both use local `M1` milestones and local `ChildLead -- "assigned to" --> M1` edges without changing their human-chosen names.

A durable cross-plan delegation from ROOT to LEFT binds, for example:

```text
reference_contract: qualified-reference-v1
repository_identity: {scheme: github-repository-id-v1, authority: github.com, id: "2001"}
plan_id: ROOT
delegation_id: LEFT-BOUNDARY
delegator_role: {repository_identity: {scheme: github-repository-id-v1, authority: github.com, id: "2001"}, plan_id: ROOT, object_kind: role, object_id: ChildLead}
delegate_role: {repository_identity: {scheme: github-repository-id-v1, authority: github.com, id: "2001"}, plan_id: LEFT, object_kind: role, object_id: ChildLead}
authority_baseline_plan_ref: <P0: exact accepted ROOT authority before the grant>
delegator_authority_source: <exact existing ROOT source at P0>
```

The endpoints differ by PlanID; the grant still must narrow ROOT's pre-existing scope. Once the grant is accepted in P1 and LEFT has accepted state C1, an operation resolves ROOT's current authority, retained grant P1, and LEFT's current Role/state at C1 separately. It cannot use P0 as proof the new grant existed, or use C1 as ROOT's authority revision.

Similarly, if ROOT's Role accepts LEFT/M1, the receipt's subject is repository 2001, PlanID LEFT, kind milestone, ID M1 at `contract_plan_ref: C1`; `accepted_by_role` is the fully qualified ROOT/ChildLead and `acceptance_authority_plan_ref` is an exact accepted ROOT revision. The two SHAs need not match. This is only reference binding; the existing acceptance rules still require real authority and evidence, and later accepted DONE projection before operational activation.

## Identity and migration counterexamples

| Case | Required resolution |
|---|---|
| LEFT and RIGHT both expose a local `ChildLead` | Keep both Roles; the full tuple selects exactly one. A bare cross-plan `ChildLead` is ambiguous and cannot authorize either. |
| Two paths define the same repository/PlanID/kind/object ID with conflicting scope | Reject ambiguity; do not combine scopes or pick the first file. Resolve through accepted authority before use. |
| A reference expects `role/X` but only `milestone/X` exists | Reject kind mismatch; an ID text match is insufficient. |
| `example/parent` is renamed/transferred but verified host/ID remains github.com/2001 | Identity stays the same; accept an unambiguous locator update and check current authority. The rename grants no additional scope. |
| The old readable repository name now resolves to ID 2999 | Reject mismatch. A same-name replacement is a new repository, even if it copied all files/commits. |
| LEFT's plan directory moves inside repository 2001 | Accepted locator change can preserve PlanID LEFT and its objects; retain exact old-revision locators. Two conflicting copies are ambiguous, not two authorities. |
| LEFT moves to repository 2002 or changes its stable PlanID | New qualified identity; explicit accepted migration/continuation may relate it, but old grants/references do not silently retarget. |
| A friendly alias `ChildLead` points to both LEFT and RIGHT, or names differ only by assumed normalization | Alias/normalization cannot select authority. Require exact declared IDs and qualified context. |
| A fork shares SHA P1 and local IDs with ROOT | Its different repository identity and independent publication state provide no inherited grant. |
| Provider uses an unsupported/unverified identity scheme | Fail closed at affected cross-repository boundary until an appropriate scheme/identity is accepted and verified. |
| Parent adopts v1 references but child still has ambiguous legacy bare strings | No silent native reinterpretation. Use explicit accepted compatibility/migration or stop affected authority use. |
| Adoption or migration exists only in a candidate | Prior accepted semantics remain current; candidate fields do not authorize their own transition. |

## First relationship in two repositories

The parent plan is ROOT in repository R-P; the child is LEARNING in repository R-C. Their identities are already known before the relationship proposal, even if the child has no accepted operational plan yet. Merely creating a child repository does not grant it authority.

| Order | Semantic content / normal publication | Reference roles |
|---|---|---|
| 0 | P0 is the accepted parent snapshot. It contains Milestone M1 and the pre-existing authority/capabilities for bounded child creation and bootstrap. | P0 is the authority baseline. It has no child relationship yet. |
| 1 | Create ordinary parent commit P1 with contract K1, exact parent Milestone/child identity, scope/limits and allowed child initialization. K1 stores `authority_baseline_plan_ref: P0`. | P1 does not contain its own SHA or C1's future SHA. |
| 2 | Existing parent authority approves exact P1; retain it, publish carrier RP1 conditionally from the accepted predecessor carrier, retain RP1, then commit its trusted journal event. | The accepted event names P1 as `parent_relationship_plan_ref`. RP1 is publication evidence, not the child pin's semantic PlanRef. |
| 3 | Create ordinary child commit C1 with child plan/Role state and `parent_plan_ref: P1`; its contract locator selects K1 in P1. | P0 authorizes creating K1, P1 contains K1, C1 contains the child's P1 pin. Every reference points to an already-known exact object. |
| 4 | Under P1's bounded existing parent authority, approve exact C1 plus its initial publication/journal/retention configuration. Retain/publish C1 and its child carrier RC1, then commit the child bootstrap journal event. | RC1 names C1; the child is operational only now. No unrelated founder or self-approval is invented. |
| 5 | A bounded operation validates current parent/child state and records the required exact parent relationship/current refs and child C1 separately. | It does not equate P0, P1, C1, RP1 or RC1. |

The dependency order is finite: P0 exists before P1 is written; P1 exists and is accepted before C1 is written; each publication carrier/event is made after its exact semantic candidate exists. No file must contain the hash of the commit containing that same file. Retained history and conditional journaled publication still follow `planning/PUBLICATION.md` and `planning/PUBLICATION_TRANSITIONS.md`.

## First relationship in one repository

Use one repository R, parent path `planning/PLAN.md` with PlanID ROOT, and child path `planning/plans/LEARNING/PLAN.md` with PlanID LEARNING. The accepted parent-authorized setup selects distinct per-plan publication refs/journal identities where independent streams are needed, using the existing configurable publication protocol. A Git commit does not become current for every plan merely because it contains their files.

| Ordinary commit / publication | Contents and meaning |
|---|---|
| P0, already accepted for ROOT | Parent authority and M1 exist. |
| P1, then normally accepted for ROOT | Parent K1 cites P0. No P1 or C1 self-reference occurs in K1. |
| C1, a later ordinary commit in the same repository | Add the LEARNING files and child pin P1. The unchanged parent K1 still cites P0. C1 need not be written into itself. |
| C1, then accepted for LEARNING under parent-authorized bootstrap | Child uses P1 while parent can remain current at P1. Each plan's journal proves its own accepted state. |
| Optional later P2 accepted for ROOT | If ROOT publishes a snapshot including child files but K1/authority are unchanged, LEARNING's P1 pin stays valid after explicit current-parent compatibility check. There is no requirement to repin to P2 solely because the repository SHA advanced. |

The child file containing P1 makes C1's hash differ from P1. That is expected: C1 is the child state, while P1 is the already accepted source of its parent relationship. The optional P2 likewise does not become a new relationship merely because its snapshot contains the child pin.

## Updates, aliases and authority counterexamples

| Situation | Required result |
|---|---|
| Parent adds an unrelated Milestone in a newer accepted snapshot | Verify K1 and relevant authority unchanged; retain P1 pin and record the newer current-parent check. |
| Parent reduces the delegated scope in accepted K2 at P3 | P3 is the new relationship revision; the child must reconcile affected work and explicitly adopt/update its pin under valid authority. Old P1 cannot preserve revoked scope. |
| Parent candidate K2 exists but is unaccepted | It is not the current relationship. Do not use proposed authority to implement/approve itself. |
| K1 embeds `parent_plan_ref: P1` before P1 exists | Reject the self-containing requirement; use prior authority baseline P0 and learn P1 from accepted publication. |
| Child pins P0 merely because K1's baseline says P0 | Reject: P0 lacks K1. The child pin must resolve the accepted containing relationship P1. |
| Child pins RP1, the publication carrier | Reject semantic-role confusion: validate RP1 as publication evidence, then pin its named semantic PlanRef P1. |
| Parent updates child-current-revision metadata and demands another child repin forever | No such cycle is required. Actual operations bind exact child snapshots separately; unchanged boundaries do not churn. |
| Same Git ancestry, submodule or copied K1 is offered as authority | Insufficient. Require explicit relationship/delegation and accepted current evidence. |
| A legacy `parent_plan_ref` cannot be classified as baseline or containing relationship | Stop affected use; resolve historical publication/authority evidence or explicitly migrate under existing authority. Do not reinterpret the field by convenience. |

The examples preserve unlimited recursive application of the same boundary rule. They do not define ancestor prerequisite/Decision branch propagation, issuer-provenance infrastructure or global satisfiability semantics.
