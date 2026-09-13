# Root role registry template

Copy this structure into `planning/ROLES.md` and replace all placeholders.

The template requires **explicit authority**, not a fixed set of substantive role names. Create only substantive Roles whose authority/responsibility must remain stable across holder changes or be granted/revoked/delegated independently.

For a **root project's first accepted state only**, the initial Role authority source may cite the founding record/publication established under `planning/PUBLICATION.md`. After that first publication, the founding exception expires and ordinary pre-existing Role authority rules apply. Any continuing founder power must itself be represented by a Role in the accepted registry.

For a child repository, initial authority may instead come from the accepted parent contract/delegation permitted by `planning/PUBLICATION.md`.

`Foreman` is the exception in this template: it is the required infrastructure Role for the autonomous execution/propagation workflow defined elsewhere in the repository. Its required presence does **not** make it a substantive superior Role and grants no technical/decision authority by itself.

## Root substantive roles

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `<RootRoleID>` | `<bind>` | `<bounded root/project scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source; founding source only for first root state>` | `<Active/Vacant>` |

Add additional root substantive Roles only when the project actually needs separately bindable authority scopes. `ProjectOwner`, `ArchitectureLead`, `ProgramLead`, and similar names are examples a project may choose; none is universally required by this template.

## Foreman infrastructure role

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `Foreman` | `<bind qualified orchestrator>` | Execution coordination for authorized work packages; plan-change propagation; scheduled follow-up. | None merely by being Foreman. Substantive decisions require a separately held Role that grants them. | `<normally none; substantive authority comes from separately held Roles>` | `<accepted source>` | `<Active/Vacant>` |

Do not omit Foreman while continuing to claim this template's autonomous orchestration/propagation behavior. A deliberate no-Foreman mode would require a separate, coherent alternative coordination contract across the repository.

A named Foreman holder is not operational until the candidate Role registry has itself become the current accepted PlanRef under `planning/PUBLICATION.md`.

## Additional/subordinate roles

| RoleID | Current holder | Parent Role | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|---|
| `<RoleID>` | `<holder or —>` | `<parent RoleID or none>` | `<bounded scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant/Retired>` |

Use only delegation capability IDs defined in `planning/NESTING.md`.

Avoid open-ended phrases such as `all normal authority`, `as needed`, `everything under X`, or `etc.` unless the referenced scope is formally defined elsewhere and linked exactly.

Do not split one real substantive authority into multiple nominal Roles unless those scopes genuinely need independent binding, revocation, delegation, or audit. Conversely, do not merge materially independent authority scopes solely to reduce Role count.
