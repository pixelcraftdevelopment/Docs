# LogTransaction

**Side:** Server

Append a transaction record to a player's history without moving money. Use for vendor receipts, audit trails, or when money has already moved via a non-PC-Banking path and you want it visible in the player's statement.

```lua
local ok = exports['pc-banking']:LogTransaction(target, txType, amount, reason, opts)
```

| Param | Type | Notes |
|-------|------|-------|
| `target` | string \| number | Identifier or server src |
| `txType` | string | Transaction type label |
| `amount` | number | Magnitude (positive integer) |
| `reason` | string | Free-form description shown in the player's statement |
| `opts.accountId` | number | Account this transaction belongs to (optional) |
| `opts.bankName` | string | Bank id (auto-resolved from accountId if omitted) |
| `opts.direction` | string | `'credit'` or `'debit'` — REQUIRED for external callers |

{% hint style="warning" %}
External exports MUST pass `opts.direction = 'credit' | 'debit'`. The export path has no inference; missing direction will result in malformed statement entries.
{% endhint %}

## Returns

* `true` on success
* `false` on missing required fields

## Recommended txType Values

For consistent statement display, match what PC-Banking uses internally:

`deposit`, `withdraw`, `transfer_in`, `transfer_out`, `card_debit`, `card_credit`, `loan_disbursement`, `loan_emi`, `interest_credit`, `fee`, `society_deposit`, `society_withdraw`

## Examples

```lua
-- Vendor receipt (money moved via a different path; just log it)
exports['pc-banking']:LogTransaction(playerSrc, 'card_debit', 250, 'Lunch at Burgershot', {
    accountId = primaryAccountId,
    bankName  = 'fleeca',
    direction = 'debit',
})

-- Cashback credit
exports['pc-banking']:LogTransaction(identifier, 'deposit', 50, 'Cashback reward', {
    accountId = 42,
    direction = 'credit',
})
```

## Notes

* Does NOT modify any balance. Pair with `AddMoney` / `RemoveMoney` if you need both the move AND the log entry.
