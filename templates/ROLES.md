# Root role registry template

Copy this structure into `planning/ROLES.md` and replace all placeholders.

| RoleID | Current holder | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|
| `ProjectOwner` | `<bind>` | `<scope>` | `<exact decisions>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant>` |
| `ArchitectureLead` | `<bind or —>` | `<scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant>` |
| `Foreman` | `<bind qualified orchestrator>` | Execution coordination for authorized work packages. | None merely by being Foreman. | `<normally none; substantive authority comes from separately held Roles>` | `<accepted source>` | `<Active/Vacant>` |

Add project-specific Roles below.

| RoleID | Current holder | Parent Role | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|---|
| `<RoleID>` | `<holder or —>` | `<parent RoleID>` | `<bounded scope>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted source>` | `<Active/Vacant/Retired>` |

Use only delegation capability IDs defined in `planning/NESTING.md`.

Avoid open-ended phrases such as `all normal authority`, `as needed`, `everything under X`, or `etc.` unless the referenced scope is formally defined elsewhere and linked exactly.
