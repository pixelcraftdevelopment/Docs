# RemoveMoney

Debit a player's account or charge a credit card.

```lua
local ok, err = exports['pc-banking']:RemoveMoney(target, amount, reason, opts)
```

| Param | Type | Notes |
|-------|------|-------|
| `target` | string \| number | Identifier or server src |
| `amount` | number | Positive integer; floored |
| `reason` | string | Free-form text shown in transaction log |
| `opts` | table \| string | `{ accountId?, cardNumber?, bankName? }` — or legacy `bankName` string |

## Behavior

* Validates frozen account, account-type withdraw limit, daily transaction count, card monthly limit
* For credit cards: charge increases `credit_balance`, validates `credit_limit` and `monthly_limit`
* For debit cards: validates account-type withdraw limits AND card monthly limit, then debits the linked account and increments `monthly_spent`
* No `opts` → debits framework `bank` balance for online player + dual-writes primary account row

## Returns

* `true` on success
* `false, errorKey` on insufficient funds, frozen account, limit exceeded

## Examples

```lua
-- Charge a vehicle repair
exports['pc-banking']:RemoveMoney(playerSrc, 1500, 'Mechanic bill')

-- Charge to a specific card
exports['pc-banking']:RemoveMoney(identifier, 200, 'POS', { cardNumber = '4929...', bankName = 'fleeca' })

-- Withdraw from secondary account
exports['pc-banking']:RemoveMoney(playerSrc, 10000, 'Withdrawal', { accountId = 42 })
```
