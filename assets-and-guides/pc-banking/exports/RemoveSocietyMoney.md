# RemoveSocietyMoney

**Side:** Server

Debit a society treasury.

```lua
local ok = exports['pc-banking']:RemoveSocietyMoney(targetOrName, amount, reason)
```

| Param | Type | Notes |
|-------|------|-------|
| `targetOrName` | string \| number | Society name OR player src (resolves to player's job) |
| `amount` | number | Positive integer |
| `reason` | string | Logged in `pc_banking_society_transactions` |

## Returns

* `true` on success
* `false` if balance insufficient, society missing, or amount invalid

## Examples

```lua
exports['pc-banking']:RemoveSocietyMoney('mechanic', 500, 'Tool purchase')
exports['pc-banking']:RemoveSocietyMoney(bossSrc, 1000, 'Office supplies')
```
