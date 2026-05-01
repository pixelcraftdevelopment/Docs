# Admin Tools

Two config blocks control admin behavior: `Config.Admin` and `Config.AdminSociety`.

## `Config.Admin`

```lua
Config.Admin = {
    enableRevert     = true,
    revertWindowDays = 7,
    requireReason    = true,
    notifyOnRevert   = true,
}
```

| Field | Type | Behavior |
|-------|------|----------|
| `enableRevert` | bool | Enables/disables transaction revert operations. |
| `revertWindowDays` | number | Revert age window in days. Older tx are rejected. |
| `requireReason` | bool | Revert actions require a non-trivial reason when enabled. |
| `notifyOnRevert` | bool | Sends notification to affected account owners on successful revert. |

`Config.Admin` access gate reuses `Config.AccountFreezing.allowedJobs` + `minGrade`.

## `Config.AdminSociety`

```lua
Config.AdminSociety = {
    enabled             = true,
    aceGroup            = 'admin',
    allowBalanceEdit    = true,
    allowAdminPayroll   = true,
    allowMemberMgmt     = true,
    notifyOnAdminAction = true,
}
```

| Field | Type | Behavior |
|-------|------|----------|
| `enabled` | bool | Master gate for ACE-based society admin callbacks. |
| `aceGroup` | string | ACE permission checked via `IsPlayerAceAllowed(src, aceGroup)`. |
| `allowBalanceEdit` | bool | Enables direct society balance adjustment callbacks. |
| `allowAdminPayroll` | bool | Enables one-shot and recurring payroll admin actions. |
| `allowMemberMgmt` | bool | Enables add/remove/update member-role admin actions. |
| `notifyOnAdminAction` | bool | Sends notifications for admin-triggered society mutations. |

## ACE Setup

Grant ACE permission matching `aceGroup` to the intended principals. Example when `aceGroup = 'admin'`:

```cfg
add_ace group.admin admin allow
add_principal identifier.<your_identifier> group.admin
```
