# AddMoney

Credit a player's account or pay down a credit card balance.

```lua
local ok, err = exports['pc-banking']:AddMoney(target, amount, reason, opts)
```

| Param | Type | Notes |
|-------|------|-------|
| `target` | string \| number | Identifier or server src |
| `amount` | number | Positive integer; floored |
| `reason` | string | Free-form text shown in transaction log |
| `opts` | table \| string | `{ accountId?, cardNumber?, bankName? }` — or legacy `bankName` string |

## Behavior

* No `opts` → credits the player's primary checking at default bank (also bumps framework `bank` balance for online players)
* `opts.accountId` → credits a specific account
* `opts.cardNumber` for a debit card → credits the linked account
* `opts.cardNumber` for a credit card → reduces credit balance (acts as payment)

## Returns

* `true` on success
* `false, errorKey` on failure (frozen account, maxBalance hit, target not found)

## Examples

```lua
-- Pay a salary into primary checking
exports['pc-banking']:AddMoney(playerSrc, 5000, 'Weekly salary')

-- Credit a specific account
exports['pc-banking']:AddMoney(identifier, 1000, 'Refund', { accountId = 42 })

-- Pay off credit card by card number
exports['pc-banking']:AddMoney(identifier, 500, 'Card payment', { cardNumber = '4929123412341234' })
```
