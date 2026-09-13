# Child role registry template

This registry is subordinate to the parent contract. It cannot create authority absent from that contract.

## Child scope owner

```text
reference_contract: qualified-reference-v1
child_plan: <qualified child plan reference; fixes all local RoleID context>
parent_plan_ref: <exact accepted parent relationship PlanRef containing the bound contract>
parent_milestone: <qualified parent milestone reference>
scope_owner_role: <RoleID>
parent_contract: <qualified parent contract reference>
parent_contract_locator: <path/link at parent_plan_ref>
```

This child-side pin differs from the parent contract's prior authority baseline. Validate the retained relationship and current parent authority before relying on its delegation; see `planning/REFERENCES.md`.

The first row's parent Role crosses a plan boundary and must be fully qualified, with its authority source at an exact accepted parent revision. Internal `ChildLead`/`SpecialistLead` references may remain local because `child_plan` fixes their context. Qualify any other external source/Role and bind its exact authority revision separately.

## Roles

Use durable holder/context references and accepted attribution rules under `planning/ROLES.md` -> **Holder attribution**. A shared account alone cannot disambiguate its contexts. Preserve the exact holder binding used for each acceptance at issuance; neither a historical parent pin nor a later rebind identifies the issuer by itself.

| RoleID | Current holder | Parent Role | Scope | Final decision authority | Delegation capabilities | Authority source | State |
|---|---|---|---|---|---|---|---|
| `<ChildLead>` | `<holder or —>` | `<qualified parent role reference>` | `<bounded child scope>` | `<exact decisions>` | `<capability IDs or none>` | `<qualified delegation; exact parent PlanRef/locator>` | `<Active/Vacant/Retired>` |
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
