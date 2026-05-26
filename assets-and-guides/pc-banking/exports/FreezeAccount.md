# FreezeAccount

**Side:** Server

Lock an account. Frozen accounts cannot send transfers, receive transfers, deposit, withdraw, or be debited via card. They remain readable.

```lua
local ok = exports['pc-banking']:FreezeAccount(accountId, frozenBy, reason)
```

| Param | Type | Notes |
|-------|------|-------|
| `accountId` | number | Account id (`pc_banking_accounts.id`). |
| `frozenBy` | string | Identifier of the actor (officer, judge, system), stored for audit. |
| `reason` | string | Free-form reason shown to owner notification. |

## Returns

- `true` on success

## Side Effects

- Sets `is_frozen = 1`, `frozen_by`, `frozen_at = NOW()`, `freeze_reason`
- If `Config.AccountFreezing.notifyOnFreeze` is enabled, owner gets a security notification with the reason

## Example

```lua
exports['pc-banking']:FreezeAccount(42, officerIdent, 'Suspected money laundering')
```

## In-Game Flow Note

In-game freeze flows should use the resource's standard UI action path so role/grade policy from `Config.AccountFreezing` is enforced automatically.
