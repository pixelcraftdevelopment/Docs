# UnfreezeAccount

Unlock a previously frozen account.

```lua
local ok = exports['pc-banking']:UnfreezeAccount(accountId, unfrozenBy)
```

| Param | Type | Notes |
|-------|------|-------|
| `accountId` | number | Account id (`pc_banking_accounts.id`). |
| `unfrozenBy` | string | Identifier of the actor (officer, judge, system), stored for audit. |

## Returns

- `true` on success

## Side Effects

- Clears `is_frozen`, `frozen_by`, `frozen_at`, `freeze_reason`
- If `Config.AccountFreezing.notifyOnUnfreeze` is enabled, owner gets a notification

## Example

```lua
exports['pc-banking']:UnfreezeAccount(42, judgeIdent)
```

## In-Game Flow Note

In-game unfreeze flows should use the resource's standard UI action path so role/grade policy from `Config.AccountFreezing` is enforced automatically.
