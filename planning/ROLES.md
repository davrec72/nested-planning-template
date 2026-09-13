# Role registry

This file records accepted Role definitions and current holder bindings for the project using this template.

A Role is a stable authority/responsibility slot. A holder is a person, chat, agent, or other execution context currently bound to that Role.

Local RoleIDs inherit the repository identity and PlanID of this registry's accepted plan. Under explicitly adopted `qualified-reference-v1`, any parent/delegate/accepting Role or authority source in another plan uses a full qualified reference and its own exact authority PlanRef under `REFERENCES.md`. Shared human names or holders never merge Roles; a path/alias is only a locator.

**The template does not prescribe a universal substantive Role vocabulary.** Create a durable substantive Role only when the project needs a stable authority/responsibility slot whose scope should survive holder changes. Names such as `ProjectOwner`, `ArchitectureLead`, `SubsystemLead`, or `Reviewer` are project choices, not built-in ontology.

A root project must still have an accepted authority chain sufficient to create/bind whatever substantive Roles it uses. The first such chain is established only by the bounded root bootstrap in `PUBLICATION.md`; after the first valid publication, ordinary non-self-authorizing Role rules apply. A child project may instead receive its boundary authority from an accepted parent contract/delegation.

`Foreman` is different: in this template it is the required **infrastructure coordination Role** for the autonomous execution/propagation workflow defined by `AGENTS.md`, `planning/CONVENTIONS.md`, work packages, and `prompts/FOREMAN.md`. Foreman is required by that workflow because it performs orchestration, targeted plan-change propagation, and scheduled follow-up. It acquires no substantive technical or decision authority merely by being Foreman.

A project that intentionally removes or replaces Foreman must also define an alternative execution/propagation mechanism and update the template-wide operational contract coherently; omitting the row alone is not a valid no-Foreman mode.

**Do not treat the placeholder rows below as active authority until the project has replaced the placeholders with accepted bindings and authority sources and that state is the current accepted PlanRef under `PUBLICATION.md`.**

## Root substantive roles

Add only the root substantive Roles this project actually needs.

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `<RootRoleID>` | `<bind>` | `<bounded project/root scope>` | `<exact decisions or none>` | `<explicitly list or none>` | `<accepted source>` | `<Active/Vacant>` |

Common role names can be useful, but do not create them merely because this template mentions them. For example, a project may have one broad root authority, several narrow peer authorities, or an externally inherited parent authority, depending on its actual governance needs.

For the **first** root authority state only, the `Authority source` may cite the accepted founding record/publication established under `PUBLICATION.md`. That exception cannot be reused for later Role changes. Any continuing power of the founder must itself be represented by an ordinary Role/binding in the first accepted state.

## Foreman infrastructure role

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `Foreman` | `<bind qualified orchestrator>` | Execution coordination for authorized work packages; plan-change propagation; scheduled follow-up. | None merely by being Foreman. May make substantive decisions only when separately holding a substantive Role that grants them. | Not used to create Lead authority; Foreman coordinates delegations already authorized by other Roles. | `<accepted source>` | `<Active/Vacant>` |

A vacant Foreman cannot perform the autonomous orchestration duties that depend on it. Do not silently substitute a plain chat or another substantive Role without updating the accepted coordination contract.

Foreman does not become operational merely because a candidate Role registry names a holder. The candidate state must first become the current accepted PlanRef through `PUBLICATION.md`.

## Delivery/subordinate roles

Add project-specific Roles here or in child-plan `ROLES.md` files.

| RoleID | Current holder | Parent Role | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|---|
| `<RoleID>` | `<holder or —>` | `<parent RoleID or none>` | `<bounded scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant/Retired>` |

## Delegation capability IDs

Use only capability IDs defined in `NESTING.md`:

```text
DECOMPOSE_SCOPE
CREATE_SUBROLES
BIND_SUBROLE_HOLDERS
DELEGATE_DECISIONS
ACCEPT_CHILD_MILESTONES
```

Absence means not authorized.

Do not write `full authority`, `as needed`, `etc.`, `all normal powers`, or similar open-ended phrases.

## Binding rules

- A holder may occupy multiple Roles.
- Durable decisions must identify the Role under which the holder acts.
- Rebinding a holder does not change Role scope or authority.
- Changing scope, final decision authority, delegation capability, or parent relationship is an authority change and requires approval under authority that existed before the change.
- A Role may be vacant. A vacant Role has no operational holder and cannot act.
- Creating a Role node in Mermaid does not bind a holder.
- Repository permissions do not bind a Role.
- Two Roles held by one underlying agent/context do not satisfy independent-review requirements merely because their names differ.
- Do not split one real substantive authority into several nominal Roles unless the scopes truly need to be granted, revoked, delegated, audited, or rebound independently.
- Do not merge distinct substantive authorities merely to reduce Role count when independent scope/binding actually matters.
- Foreman coordinates execution but does not acquire the substantive decision authority of the Roles whose work it coordinates.
- A proposed Role/binding change is not operative until the exact candidate planning state containing it is approved and published as current under `PUBLICATION.md`.

## Foreman holder qualification

Before binding a holder to `Foreman`, verify that the holder's environment can:

1. delegate tasks to other agents/contexts;
2. schedule future follow-up tasks/checks;
3. read the canonical plan/role records and exact PlanRefs;
4. discover and validate the current accepted PlanRef under `PUBLICATION.md`;
5. track multiple concurrent work packages without silently losing their bindings;
6. surface inability to continue rather than pretending asynchronous work will complete without a scheduled mechanism.

If any required capability is absent, do not bind that holder to `Foreman`.
