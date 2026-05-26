# GetSocietyBalance

**Side:** Server

Read a society treasury balance.

```lua
local balance = exports['pc-banking']:GetSocietyBalance(targetOrName)
```

| Param | Type | Notes |
|-------|------|-------|
| `targetOrName` | string \| number | Society name OR player src (resolves to player's job) |

## Returns

* `number` — balance (integer)
* `0` if society doesn't exist

## Examples

```lua
local cash = exports['pc-banking']:GetSocietyBalance('police')

-- By the calling player's job
local mySocietyCash = exports['pc-banking']:GetSocietyBalance(playerSrc)
```
