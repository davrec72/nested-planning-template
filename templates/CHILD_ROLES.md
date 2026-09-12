# Child role registry template

This registry is subordinate to the parent contract. It cannot create authority absent from that contract.

## Child scope owner

```text
plan_id: <child PlanID>
parent_plan_ref: <exact parent PlanRef>
parent_milestone: <parent MilestoneID>
scope_owner_role: <RoleID>
parent_contract: <path/link>
```

## Roles

| RoleID | Current holder | Parent Role | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|---|
| `<ChildLead>` | `<holder or —>` | `<parent RoleID>` | `<bounded child scope>` | `<exact decisions>` | `<capability IDs or none>` | `<accepted delegation>` | `<Active/Vacant/Retired>` |
| `<SpecialistLead>` | `<holder or —>` | `<ChildLead>` | `<strict subset>` | `<exact decisions or none>` | `<capability IDs or none>` | `<accepted child delegation>` | `<Active/Vacant/Retired>` |

## Rules

- A subordinate Role's scope must be a subset of its parent Role's accepted scope.
- A subordinate Role cannot receive a delegation capability its parent lacks.
- A subordinate Role cannot receive a substantive decision authority its parent does not possess.
- `DELEGATE_DECISIONS` transfers a defined final decision scope downward; do not leave simultaneous final authority over the identical scope at parent and child unless the grammar explicitly defines a joint mechanism.
- Rebinding a holder does not change scope or authority.
- Vacant Roles cannot act.
- Two Roles held by one agent/context do not create review independence.
- Foreman may coordinate the work of these Roles but does not become their substantive technical authority.
