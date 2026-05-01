# Account Freezing

Law-enforcement freeze/unfreeze gate. Defines who can freeze accounts, which account classes can be frozen, and notification behavior.

```lua
Config.AccountFreezing = {
    enabled            = true,
    allowedJobs        = { 'police', 'fbi' },
    minGrade           = 3,
    canFreezeShared    = true,
    canFreezeBusiness  = true,
    notifyOnFreeze     = true,
    notifyOnUnfreeze   = true,
}
```

| Field | Notes |
|-------|-------|
| `enabled` | Gate for job-checked in-game/admin freeze tooling. If `false`, those gated flows deny access; trusted direct exports can still be called by server scripts. |
| `allowedJobs` | Exact job name allowlist used by the gate (exact match against `job.name`). |
| `minGrade` | Numeric minimum grade required by the gate (`job.grade >= minGrade`). |
| `canFreezeShared` | Applies to gated in-game freeze flow only. If `false`, accounts with `account_class = 'shared'` cannot be frozen there. |
| `canFreezeBusiness` | Applies to gated in-game freeze flow only. If `false`, accounts with `account_class = 'business'` cannot be frozen there. |
| `notifyOnFreeze` | When `true`, freeze action sends owner a security notification with reason text. |
| `notifyOnUnfreeze` | When `true`, unfreeze action sends owner a security notification. |

## Who Can Freeze

Standard in-game freeze actions check the caller's:

1. Job name is in `allowedJobs`
2. Job grade >= `minGrade`
3. Target account class is allowed (per `canFreezeShared` / `canFreezeBusiness`)

Using the [`FreezeAccount`](../exports/FreezeAccount.md) export directly does not enforce these gates. Exports are intended for trusted server-side scripts (for example court-order automation or fraud-detection pipelines).

## Adding Departments

```lua
Config.AccountFreezing.allowedJobs = { 'police', 'fbi', 'dea', 'irs' }
```

Each new job name must match the framework job key.
