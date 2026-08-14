# GetAvailableBalance

**Side:** Server

Returns an account's spendable balance, including any overdraft available for the requested debit channel.

```lua
local available = exports['pc-banking']:GetAvailableBalance(target, opts)
```

| Param | Type | Notes |
|-------|------|-------|
| `target` | string \| number | Player identifier or server source. |
| `opts` | table | Optional account-selection and overdraft-channel flags; see below. |

### `opts` flags

| Flag | Type | Behavior |
|------|------|----------|
| `accountId` | number | Uses that specific account. |
| `cardNumber` | string | Resolves the account linked to that card. |
| `channel` | string | Debit path used to evaluate overdraft eligibility. Defaults to `external`. Typical values are `transfer`, `withdrawal`, `cardPurchase`, `atm`, `savings`, `loanPayment`, `creditPayment`, `standingOrder`, `fee`, `society`, and `admin`. |

The account selection matches [`GetBalance`](GetBalance.md). The returned amount is never negative. It equals the ledger balance plus the eligible overdraft limit for the selected channel. A disabled or ineligible channel adds no overdraft room.

```lua
local available = exports['pc-banking']:GetAvailableBalance(identifier, {
    accountId = 142,
    channel = 'transfer',
})
```
