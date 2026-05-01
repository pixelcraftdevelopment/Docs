# Global Limits

Server-wide safeguards in `pc-banking/config/config.lua`. These apply in addition to account/card-type rules.

## Schema

```lua
Config.GlobalDeposits = {
    maxPerTransaction = 500000,
    dailyLimit        = 2000000,
}

Config.GlobalWithdrawals = {
    maxPerTransaction = 500000,
    dailyLimit        = 2000000,
}

Config.GlobalTransfers = {
    maxPerTransaction  = 1000000,
    dailyLimit         = 5000000,
    cooldownMs         = 2000,
    allowOffline       = true,
    allowSelfCrossBank = true,
}
```

## Field Reference

### `Config.GlobalDeposits`

| Field | Type | Behavior |
|-------|------|----------|
| `maxPerTransaction` | number | Enforced only when `> 0`. |
| `dailyLimit` | number | Enforced only when `> 0` (daily sum of `deposit` tx for sender identifier). |

### `Config.GlobalWithdrawals`

| Field | Type | Behavior |
|-------|------|----------|
| `maxPerTransaction` | number | Enforced only when `> 0`. |
| `dailyLimit` | number | Enforced only when `> 0` (daily sum of `withdraw` tx for sender identifier). |

### `Config.GlobalTransfers`

| Field | Type | Behavior |
|-------|------|----------|
| `maxPerTransaction` | number | Hard cap for transfers. `0` effectively blocks positive transfers. |
| `dailyLimit` | number | Enforced only when `> 0` (daily sum of `transfer_out` for sender identifier). |
| `cooldownMs` | number | Transfer action cooldown window. `0` removes cooldown. |
| `allowOffline` | bool | If `false`, recipient must be online. |
| `allowSelfCrossBank` | bool | If `false`, self-transfer path (`fromId == toIdentifier`) is blocked. |

## Notes

1. Global checks and account/card checks both run.
2. Transfer limits are enforced in both direct transfer and request-accept transfer paths.
3. Deposit/withdraw `maxPerTransaction` uses `> 0` gating; transfer `maxPerTransaction` does not.
