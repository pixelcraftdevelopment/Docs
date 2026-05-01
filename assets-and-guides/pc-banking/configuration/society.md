# Society Configuration

Defined in `pc-banking/config/society.lua`. This file controls seeded role permissions, grade-based defaults, and society-type templates.

## `Config.DefaultRoles`

Used when creating non-job-locked societies (for example player-created groups/businesses).

```lua
Config.DefaultRoles = {
  {
    name = 'owner',
    label = 'Owner',
    level = 3,
    canWithdraw = true,
    canDeposit = true,
    canManageMembers = true,
    canManageRoles = true,
    canManagePayroll = true,
    canViewBalance = true,
    withdrawLimit = 0,
  },
}
```

| Field | Type | Notes |
|-------|------|-------|
| `name` | string | Role key stored in DB |
| `label` | string | Role label shown in UI |
| `level` | number | Role hierarchy (higher = stronger) |
| `canWithdraw` | bool | Permit society withdrawals |
| `canDeposit` | bool | Permit society deposits |
| `canManageMembers` | bool | Add/remove members |
| `canManageRoles` | bool | Create/update/delete roles |
| `canManagePayroll` | bool | Run payroll/role payouts |
| `canViewBalance` | bool | See society balance and related data |
| `withdrawLimit` | number | Per-withdraw cap for this role (`0` = unlimited) |

## `Config.DefaultGradePermissions`

Used when seeding grade roles for framework job-locked societies.

```lua
Config.DefaultGradePermissions = {
  [0] = { canWithdraw = false, canDeposit = true, ... },
  [4] = { canWithdraw = true,  canDeposit = true, ... },
}
```

| Field | Notes |
|-------|-------|
| grade key (`[0]`, `[1]`, ...) | Framework grade number |
| permission object | Same permission fields as `DefaultRoles` |

If an exact grade key is missing, the seeder chooses the closest lower configured grade (fallback to grade `0`).

## `Config.SocietyTypes`

Single source of type templates used for metadata and startup syncing.

```lua
Config.SocietyTypes = {
  ['police'] = {
    label = 'Law Enforcement',
    maxMembers = 50,
    jobLocked = true,
    jobName = 'police',
    autoMembership = true,
  },
}
```

| Field | Type | Notes |
|-------|------|-------|
| type key | string | Society type id (`police`, `ems`, `gang`, etc.) |
| `label` | string | Human label for UI display |
| `maxMembers` | number | Default member cap for that type |
| `jobLocked` | bool | Restricts society membership to matching framework job |
| `jobName` | string | Framework job key linked to that society type |
| `autoMembership` | bool | Auto-resolves members by job data (instead of explicit list only) |

## Runtime Notes

1. On startup, framework jobs are synced into societies and grade roles are seeded in DB.
2. For framework jobs, `job_locked=1` and `auto_membership=1` are enforced by startup sync.
3. `Config.SocietyTypes` mainly provides overrides/metadata (label, caps, job mapping template).
4. `withdrawLimit` is enforced per role during society withdrawals.
5. Payroll permission for job-locked societies is tied to boss-grade behavior in runtime checks.
