# Roles & Permissions

Defined in `pc-mechanic/config/config.lua` under `Config.Roles`. Each role has a level, a list of mapped framework grades, and a flat permissions table that gates every action.

## Schema

```lua
Config.Roles = {
    availableRoles = {
        {
            name              = "owner",
            label             = "Owner",
            level             = 3,
            availableInTablet = false,
            frameworkGrades   = { 4 },
            permissions       = { --[[ flag = boolean | { roles } ]] }
        },
        {
            name            = "manager",
            label           = "Manager",
            level           = 2,
            frameworkGrades = { 3 },
            permissions     = { --[[ ... ]] }
        },
        {
            name            = "mechanic",
            label           = "Mechanic",
            level           = 1,
            frameworkGrades = { 2 },
            permissions     = { --[[ ... ]] }
        },
        {
            name            = "novice",
            label           = "Novice",
            level           = 0,
            frameworkGrades = { 0, 1 },
            permissions     = { --[[ ... ]] }
        }
    },
    adminRole = {
        name            = "server_admin",
        label           = "Server Admin",
        level           = 99,
        frameworkGrades = { 4 },
        permissions     = { --[[ ... ]] }
    }
}
```

### Role Entry Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `name` | string | Internal role key. Referenced by every permission list (`canHire`, `canFire`, `canPromote`, `canDemote`) |
| `label` | string | Display name shown in tablet UI |
| `level` | number | Numeric hierarchy. Higher levels outrank lower levels for general comparisons. Server admin = 99, owner = 3, manager = 2, mechanic = 1, novice = 0 |
| `availableInTablet` | boolean (optional) | Whether the tablet UI lists this role as a hire/fire target. Defaults to true for non-owner roles. Owner is `false` by default to prevent multiple owners being created via tablet |
| `frameworkGrades` | table | Array of framework job grade numbers that map to this role. First match wins — two roles cannot share the same grade |
| `permissions` | table | Flat permission flag map. See the full reference below |

## Levels and Default Grade Mapping

| Role | Level | Framework grades |
|------|-------|------------------|
| novice | 0 | 0, 1 |
| mechanic | 1 | 2 |
| manager | 2 | 3 |
| owner | 3 | 4 |
| server_admin | 99 | 4 |

A higher level can manage lower levels — but only the roles named in their `canHire` / `canFire` / `canPromote` / `canDemote` arrays.

## Permission Flags

| Flag | Default by role | Purpose |
|------|----------------|---------|
| `canFrameworkHire`/`Fire`/`Promote`/`Demote` | All four are true for every role by default | Whether the role can act on the framework's job system |
| `canHire = { roles }` | owner: all lower; manager: mechanic+novice; mechanic: novice; novice: empty | Internal roles this role can hire |
| `canFire`, `canPromote`, `canDemote` | Same shape as `canHire` | Role-targeted action lists |
| `canAccessManagement` | All shop roles: true | Open the management page |
| `canAccessSettings` | All shop roles: true | Settings sub-page (some content gated by `canChangeBusinessSettings`) |
| `canChangeBusinessSettings` | owner only | Modify business-side toggles |
| `canAccessTablet` | All shop roles: true | Open the tablet at all |
| `canManageOrders`, `canClaimOrders` | All shop roles: true | Order workflow |
| `canDeleteOrders` | manager+, false for mechanic/novice | Delete orders |
| `canViewAllBills` | manager+, false below | See bills outside your own |
| `canViewAllOrders` | owner only | See others' orders |
| `canViewAllShopOrders` | manager+, mechanic/novice false | See shop-wide parts orders |
| `canViewFunds` | All shop roles: true | See society balance |
| `canWithdrawFunds`, `canDepositFunds` | manager+ only | Move society money |
| `canViewAnalytics` | All shop roles: true | Analytics page |
| `canInstallParts`, `canManageInvoices`, `canServiceVehicles`, `canInspectVehicles`, `canApplyTuning`, `canPurchaseParts`, `canInstallNitrous`, `canToggleDuty` | All shop roles: true | Action permissions |
| `allowSocietyPay` | All shop roles: true | Allow society pay on this role's invoices |
| `allowFreeService` | manager+, false for mechanic/novice | Allow waiving the bill |

## How Permissions Combine With Shop Settings

Some permissions exist on both the **role** and the **shop**:

- `allowSocietyPay`: true required on **both** the role and the shop for society pay to be available.
- `allowFreeService`: same — both must be true.

This double-gate prevents a manager from waiving the bill at a shop that doesn't permit free service, and vice versa.

## Server Admin

The `adminRole` is special:

- Level 99 — outranks all in-shop roles
- `canHire/Fire/Promote/Demote` includes `owner`, `manager`, `mechanic` (note: not novice — admins should typically only manage senior staff; adjust if needed)
- All action and fund permissions enabled
- Required for `Config.LetAdminsUseTablets = true` to grant tablet access without holding a mechanic job

## Adding a New Role

1. Add a new entry to `Config.Roles.availableRoles` with a unique `name` and a level fitting your hierarchy
2. Set `frameworkGrades` to the framework grade(s) you want mapped to this role
3. Set `permissions` — start by copying a similar role and trimming
4. Update other roles' `canHire`/`canFire`/`canPromote`/`canDemote` lists to include the new role where you want them to be able to manage it
5. Restart `pc-mechanic`

{% hint style="warning" %}
`frameworkGrades` is the **only** thing that determines which framework grade lands on which internal role. Two roles cannot share the same grade — first match wins. If you want a finer split than your framework supports, set `Config.InternalFrameworkJobsystem = false` and manage employees in PC-Mechanic's internal table instead.
{% endhint %}
