# AddSocietyMoney

Credit a society treasury.

```lua
local ok = exports['pc-banking']:AddSocietyMoney(targetOrName, amount, reason)
```

| Param | Type | Notes |
|-------|------|-------|
| `targetOrName` | string \| number | Society name (`'police'`) OR player src (resolves to player's job) |
| `amount` | number | Positive integer |
| `reason` | string | Logged in `pc_banking_society_transactions` |

## Returns

* `true` on success
* `false` if society doesn't exist, amount invalid, or job lookup failed

## Side Effects

* Inserts a `deposit` row into `pc_banking_society_transactions` with `balance_after`
* Calls `syncLegacySocietyBalance` to mirror to legacy tables (`management_funds`, `addon_account_data`, `okokbanking_account_data`) when corresponding compat shims are enabled

## Examples

```lua
-- Pay fine into police treasury
exports['pc-banking']:AddSocietyMoney('police', 500, 'Speeding ticket')

-- Pay into the society of whatever job the player has
exports['pc-banking']:AddSocietyMoney(playerSrc, 2000, 'Sale commission')
```
