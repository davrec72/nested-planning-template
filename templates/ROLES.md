# Root role registry template

Copy this structure into `planning/ROLES.md` and replace all placeholders.

The template requires **explicit authority**, not a fixed set of role names. Create only Roles whose authority/responsibility must remain stable across holder changes or be granted/revoked/delegated independently.

## Root roles

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `<RootRoleID>` | `<bind>` | `<bounded root/project scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant>` |

Add additional root Roles only when the project actually needs separately bindable authority scopes. `ProjectOwner`, `ArchitectureLead`, `ProgramLead`, and similar names are examples a project may choose; none is universally required by this template.

## Optional Foreman

Add this row only if the project uses the orchestration workflow in `prompts/FOREMAN.md`:

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `Foreman` | `<bind qualified orchestrator>` | Execution coordination for authorized work packages. | None merely by being Foreman. | `<normally none; substantive authority comes from separately held Roles>` | `<accepted source>` | `<Active/Vacant>` |

Foreman is a workflow convenience with an explicit contract, not a universal planning role.

## Additional/subordinate roles

| RoleID | Current holder | Parent Role | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|---|
| `<RoleID>` | `<holder or —>` | `<parent RoleID or none>` | `<bounded scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant/Retired>` |

Use only delegation capability IDs defined in `planning/NESTING.md`.

Avoid open-ended phrases such as `all normal authority`, `as needed`, `everything under X`, or `etc.` unless the referenced scope is formally defined elsewhere and linked exactly.

Do not split one real authority into multiple nominal Roles unless those scopes genuinely need independent binding, revocation, delegation, or audit. Conversely, do not merge materially independent authority scopes solely to reduce Role count.
