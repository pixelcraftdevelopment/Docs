# GetBalance

**Side:** Server

Read a player's bank balance.

```lua
local balance = exports['pc-banking']:GetBalance(target, opts)
```

| Param | Type | Notes |
|-------|------|-------|
| `target` | string \| number | Identifier or server src |
| `opts` | table | `{ accountId?, cardNumber? }` — optional |

## Behavior

* No `opts` → returns framework `bank` balance for online players (falls back to DB scalar lookup for offline)
* `opts.accountId` → returns balance of a specific account
* `opts.cardNumber` (debit card) → returns linked account balance
* `opts.cardNumber` (credit card) → returns `credit_limit - credit_balance` (available credit)

## Returns

* `number` — balance (always integer cents)
* `0` if target / account not found

## Examples

```lua
local primary = exports['pc-banking']:GetBalance(playerSrc)

local savings = exports['pc-banking']:GetBalance(identifier, { accountId = 142 })

local available = exports['pc-banking']:GetBalance(identifier, { cardNumber = '5555...' })
```
