# Role registry

This file records accepted Role definitions and current holder bindings for the project using this template.

A Role is an authority/responsibility slot. A holder is a person, chat, agent, or other execution context currently bound to that Role.

**Do not treat the placeholder rows below as active authority until the project has replaced the placeholders with accepted bindings and authority sources.**

## Root roles

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `ProjectOwner` | `<bind>` | Project goals, major priorities, top-level scope, major resources and top-level delegation. | Decisions explicitly retained by the owner. | `<explicitly list or none>` | `<accepted source>` | Vacant until bound |
| `ArchitectureLead` | `<bind>` | Project-wide architecture and plan topology within delegated owner scope. | Cross-scope architectural decisions explicitly delegated here. | `<explicitly list or none>` | `<accepted source>` | Vacant until bound |
| `Foreman` | `<bind qualified orchestrator>` | Execution coordination for authorized work packages. | None merely by being Foreman. May make substantive decisions only when separately holding a Role that grants them. | Not used to create Lead authority; Foreman coordinates delegations already authorized by other Roles. | `<accepted source>` | Vacant until qualified holder bound |

## Delivery/subordinate roles

Add project-specific Roles here or in child-plan `ROLES.md` files.

| RoleID | Current holder | Parent Role | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|---|
| `<RoleID>` | `<holder or —>` | `<parent RoleID>` | `<bounded scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant/Retired>` |

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
- Foreman coordinates execution but does not acquire the substantive decision authority of the Roles whose work it coordinates.

## Foreman holder qualification

Before binding a holder to `Foreman`, verify that the holder's environment can:

1. delegate tasks to other agents/contexts;
2. schedule future follow-up tasks/checks;
3. read the canonical plan/role records and exact PlanRefs;
4. track multiple concurrent work packages without silently losing their bindings;
5. surface inability to continue rather than pretending asynchronous work will complete without a scheduled mechanism.

If any required capability is absent, do not bind that holder to `Foreman`.
