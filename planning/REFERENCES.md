# Cross-plan references and parent relationship revisions

This contract supplements the existing roadmap and publication rules. Exact Git SHAs identify content; accepted currentness comes from the configured publication journal and retained evidence under `PUBLICATION.md` and `PUBLICATION_TRANSITIONS.md`. A source branch, copied repository or shared Git ancestry does not establish planning authority.

## Adoption: qualified-reference-v1

`qualified-reference-v1` is a separately adopted reference contract. It does not change Mermaid `plan-grammar-v2` syntax or introduce a second identity/currentness registry or journal. An instantiated plan explicitly declares `reference_contract: qualified-reference-v1` and its identity in an accepted published PlanRef before using these semantics. A template header or unaccepted migration does not activate them.

Each participating plan declares this context in its accepted plan header:

```text
reference_contract: qualified-reference-v1
repository_identity: {scheme: github-repository-id-v1, authority: <GitHub host>, id: <numeric repository ID>}
repository_locator: <current readable owner/repo or URL>
plan_id: <repository-local stable PlanID>
```

The flow-style objects in this document show named fields, not a new Mermaid syntax. `repository_identity.scheme`, `.authority` and `.id` correspond to the identity scheme, provider authority/host, and stable machine repository ID. For this GitHub scheme, serialize the ID losslessly as a decimal digit string without leading zeroes; do not round it through a limited-precision number. Identity equality compares all three fields under the adopted scheme; it does not compare a locator or path. Verify the authority as the provider's canonical host, rather than substituting an unverified URL alias.

For GitHub-family repositories use `github-repository-id-v1`, the actual hosting authority (for example `github.com` or a GHES host), and the provider's immutable numeric repository ID. Validate the identity through provider evidence under the existing trust configuration; a self-authored header alone is insufficient. A readable rename/transfer may preserve identity only when the same host and machine ID are verified. Deletion/recreation at the old locator with a new ID is a different repository. A fork/copy/export has its own identity and gains no authority from copied IDs or history.

Another provider requires an explicitly adopted scheme with an equivalently stable provider/authority-scoped machine identity and verification rules. Unsupported schemes, unverified IDs, or host/ID mismatches fail closed for affected cross-repository use. Do not invent a repository UUID/URI or assume two providers' identical numbers identify the same repository.

## Qualified enduring objects

A durable reference crossing any plan boundary has this full form, including same-repository boundaries:

```text
repository_identity: {scheme: <adopted scheme>, authority: <provider authority>, id: <stable machine ID>}
plan_id: <repository-local stable PlanID>
object_kind: plan | role | milestone | gate | decision | data | contract | delegation
object_id: <plan-local stable ID; omitted or none for object_kind=plan>
```

`contract` and `delegation` identify durable relationship/authority records; they are not additional roadmap node types. Other kinds require an explicitly supported contract. A Role `X` is not Milestone `X`: kind participates in resolution. This does not relax the existing Mermaid syntax requirement that one diagram identifier denotes one node/type.

PlanIDs are stable and cannot be reused for a different plan within one repository identity. Object IDs are stable and cannot be reused for a different object of the same kind within one PlanID. Distinct plans/repositories may freely reuse `ChildLead`, `M1`, or any other human-chosen name. Labels may change without changing IDs. Preserve retired identities as history rather than reassigning them.

Compare PlanIDs and object IDs by their exact declared spelling. Do not silently normalize two local names into one authority-bearing object. A display alias is not a substitute for the declared ID.

A short local ID is valid only when its containing record fixes **one repository identity and one PlanID**, and its field fixes the expected kind. Local roadmap nodes inherit their accepted plan header; local Role registry rows inherit the same plan's context. A bare `ChildLead` in a cross-plan delegation does not inherit whichever plan the reader prefers. Use the full tuple for every cross-plan endpoint, parent Milestone/Role/contract and cross-plan acceptance/return authority.

Durable locators may accompany the tuple: repository name/URL, plan path, record path and friendly aliases aid discovery. They are not resolver keys and cannot broaden scope. A move within a repository can preserve a PlanID/object only through an accepted, unambiguous locator update with the same identity; an ID change denotes a new object. A cross-repository move denotes a new qualified identity, even if files/IDs are copied. Explicit accepted migration can relate predecessor and successor, but old references never silently retarget. Alias collisions and duplicate definitions of the same qualified object fail closed; do not choose the first matching file or merge their authority.

## Exact revision and authority resolution

The qualified tuple identifies the enduring object. A separately named exact `plan_ref` identifies its content revision; publication evidence establishes acceptance/currentness. Neither a PlanRef nor a holder identity is part of the enduring object key. A local ID, a matching SHA, or a correct tuple alone does not grant authority.

Resolve a durable reference by checking:

1. the repository's machine identity against provider evidence, not just the locator;
2. the repository-local PlanID against the accepted plan header at its bound locator, rejecting contradictory/duplicate definitions;
3. the expected kind and local object ID in that plan (or the plan itself when `object_kind: plan`);
4. the separately cited exact accepted PlanRef and required retained publication evidence for the revision being judged, plus current publication/authority where the action depends on current permission.

For separate plans, resolve each from its own configured accepted publication context. Do not infer that a commit accepted for one plan is accepted for every plan whose files happen to be in its tree. A locator resolving to a different host/machine ID must fail, even when names or commits match.

For authority-bearing records, distinguish the subject plan/contract revision from each acting/delegating/accepting Role's authority revision. Every cross-plan Role endpoint is qualified and every relied-upon external authority source binds its own exact PlanRef and source locator. For example, a child Milestone's `contract_plan_ref` is in the child plan; a parent accepting Role's `acceptance_authority_plan_ref` is in the parent plan. They are not forced equal. Check the accepted Role/binding and exact scope under existing rules; this reference contract supplies no new issuer-provenance infrastructure or authority grant.

An existing shared field such as `plan_ref` has only the containing record's explicit plan context. It cannot stand in for both sides of a cross-plan delegation. A proposed grant cites the delegator's prior `authority_baseline_plan_ref`; at actual use resolve the delegate's accepted Role/state and current delegator/relationship authority separately. An intended child Role may be named before child bootstrap, but cannot act until its own state is validly accepted.

## Reference migration and compatibility

Adoption is an explicit forward planning change under pre-existing authority and the existing publication protocol. Identify affected records, resolve old strings using historical evidence, record qualified identities and their distinct exact revision meanings, and migrate parent/child boundary references together or with an explicit accepted compatibility mapping. Retain historical v2 records unchanged and with their original meaning. Do not silently reinterpret old bare cross-plan strings after adoption.

Native parent/child resolution requires compatible adopted reference semantics or an explicit accepted compatibility/migration mapping. Unsupported or ambiguous legacy authority references are opaque/fail-closed for the affected operation until resolved. A mapping names exact old/new identities, revisions and bounded applicability; it does not merge scopes or turn a copied plan into the original. Proposed/unpublished adoption is not current, and inability to verify one boundary does not grant an unrelated fallback authority.

## Parent authority baseline, accepted relationship and child pin

These revision roles are distinct:

| Reference | Where it is recorded/resolved | Meaning |
|---|---|---|
| `authority_baseline_plan_ref` | Parent-side contract/delegation | Exact **prior accepted parent PlanRef** whose existing authority permits creation/change of this relationship. It need not contain the new relationship. |
| `parent_relationship_plan_ref` | Publication handoff/validation evidence, after acceptance | Exact accepted parent PlanRef containing the relationship/contract/delegation being bound. It is learned from publication, not embedded as its own commit SHA inside the new parent contract. |
| `parent_plan_ref` | Child-side `PARENT.md`, child plan/Role headers and nested work binding | Child's pin to that accepted relationship PlanRef. For the initial relationship, this equals `parent_relationship_plan_ref`, not the earlier authority baseline. |
| `parent_current_plan_ref` | Current action/reconciliation evidence | Latest valid accepted parent state from its publication journal. Check that it still supports the pinned relationship and authority; it need not equal the historical child pin. |
| Child `plan_ref` | Exact child publication/action evidence | Child's own accepted snapshot. It need not equal any parent SHA, even when the two plans share Git storage. |

`child_parent_pin` is the conceptual name for the existing child-side `parent_plan_ref` field; it equals the bound `parent_relationship_plan_ref`. The latest relationship revision is the accepted parent revision that last materially changed this boundary, not every newer unrelated parent snapshot. These descriptive revision roles do not add fields to the publication journal: the existing event's exact semantic `plan_ref` supplies the accepted revision.

The parent contract names its stable contract identity, exact authority baseline/source, parent Milestone, child identity, delegated scope and authority limits. It MUST NOT require its own containing `parent_relationship_plan_ref` or the not-yet-existing child snapshot SHA. The child pin supplies the later relationship revision once that revision is accepted. Expected child identity is not proof that a child Role/state already exists; it becomes operational only through valid child initialization/publication.

The baseline proves authority for the transition, not perpetual current permission. At use, validate both retained pinned relationship evidence and current parent/child authority. A revoked, incompatible or ambiguous relationship cannot continue merely because an old pin still contains a grant. A candidate parent edit cannot validate itself by citing its new authority.

## Finite first-relationship sequence

Let P0, P1 and C1 abbreviate distinct exact Git commits in this explanation. Operational records use full SHAs and exact retained locators. Neither a merge nor an unjournaled ref update substitutes for publication acceptance.

1. **Resolve P0.** The current accepted parent already contains the parent Milestone and an authorized Role with the capabilities needed to create/change the child boundary. Validate its journal, retained snapshots/carriers and authority. If creating a new child, existing parent authority must also cover the bounded child bootstrap, initial Role/binding state, and publication/journal/retention trust setup required by `PUBLICATION.md`.
2. **Prepare the parent candidate P1.** Add the parent contract/delegation with `authority_baseline_plan_ref: P0` and the exact pre-existing authority source. Name the child identity/plan location and intended child boundary Role; do not insert P1's own SHA or an unknown C1 SHA into this candidate.
3. **Approve and publish P1.** Pre-existing P0 authority approves the exact P1 candidate. Retain the candidate and carrier evidence and commit its trusted publication event under the canonical `plan-publication-v1` procedure in `planning/PUBLICATION.md` and `planning/PUBLICATION_TRANSITIONS.md`. Only then does P1 become an accepted `parent_relationship_plan_ref`.
4. **Prepare the child candidate C1.** Its `parent_plan_ref` pins P1; its parent-contract locator resolves to the exact contract in P1. Its own initial plan/Role state stays within that grant. C1 does not include its own SHA. For a new child, obtain the required bounded parent-authorized approval of the exact C1 and its initial trust contract after C1 exists; do not pretend P1 already approved an unknown C1.
5. **Publish C1.** Establish its accepted state under the existing child-bootstrap/publication procedure (or normal publication for an already initialized child). Retain required exact evidence. Only now may dependent child operation rely on its accepted Role/state plus the parent relationship.
6. **Bind actual operations.** Retrieve current parent and child publication evidence and bind the appropriate exact refs separately. Parent authority/current-state checks and the existing contract/delegation limits still apply. Neither side must add a pointer to the other side's new containing SHA on every update.

This needs a finite parent semantic commit, a finite child semantic commit, and their normal publication carriers/events. The actual number of retention/approval carrier steps follows the already-configured publication protocol; there is no hash fixed-point search.

### Two repositories

P0/P1 are in the parent repository; C1 is in the child repository. Each plan uses its own accepted publication state. The child can fetch P1 through retained parent evidence, and later operations can fetch C1 through retained child evidence. Independent Git histories do not need to be joined. A fork/submodule pointer cannot replace either authority chain.

### One repository

Parent and child may use different plan paths in the same Git repository. P1 adds the parent relationship; a later ordinary C1 commit adds the child state/pin to P1. Co-location does not make all plans share one accepted current PlanRef automatically: bind each plan to its configured publication stream and trust records. If independent streams are used, configure distinct publication refs/journal identities through the existing permitted configuration, not conflicting claims on one CURRENT payload.

The child's C1 can be published while the parent's accepted state remains P1. If a later parent publication P2 includes the same unchanged relationship plus the child files, P2 is a newer parent current snapshot, not a new semantic relationship just because its Git SHA differs. The child can retain its valid P1 pin after checking the unchanged boundary and current authority. It does not need to update to P2 simply because its own pin made a new repository commit.

## Relationship updates and stale pins

For a material parent boundary change, resolve the then-current accepted parent as the new authority baseline, create a new parent contract revision under that baseline's authority, approve/publish the exact successor, and notify affected child work. The child then explicitly updates its pin to the new accepted relationship revision and publishes that change under valid authority. Preserve prior contracts, pins and their accepted publication evidence as history.

Changing an outcome, criteria, parent identity/Milestone, delegated scope/authority or another parent-visible boundary cannot be treated as an internal child edit. An old child pin cannot weaken or evade the new current boundary. Until compatibility, work impact and any required child adoption are resolved, stop the affected dependent operation and escalate; do not guess which reference wins.

Unrelated parent changes do not force child churn. Record the current parent PlanRef and comparison showing that the pinned relationship and relevant authority remain applicable. Likewise, an internal child revision does not require a parent contract update when the boundary is unchanged. For an actual dispatch/decision/acceptance, still bind the exact child revision being used.

## Legacy parent reference migration

An existing ambiguous parent-side `parent_plan_ref` is not automatically a baseline or relationship reference. Inspect its exact historical contract/publication/authority evidence. In a new accepted contract revision, explicitly record `authority_baseline_plan_ref` with its source and recover the accepted relationship revision from publication evidence. The child-side `parent_plan_ref` is the pin to that relationship revision. Preserve old records; do not rewrite historical SHAs or infer authority from matching filenames/branches.

If the historical distinction cannot be established, stop affected cross-plan use and resolve it under existing authority. Do not invent a self-containing SHA or backdate acceptance to make the fields appear equal.
