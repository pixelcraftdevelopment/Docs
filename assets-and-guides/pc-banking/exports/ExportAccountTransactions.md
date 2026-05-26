# ExportAccountTransactions

**Side:** Server

Paginated transaction history for an account.

```lua
local rows = exports['pc-banking']:ExportAccountTransactions(accountId, opts)
```

| Opt | Type | Notes |
|-----|------|-------|
| `limit` | number | Default 100, max 1000 |
| `offset` | number | Default 0 |
| `dateFrom` | string | MySQL datetime; inclusive |
| `dateTo` | string | MySQL datetime; inclusive |
| `type` | string | Filter by transaction type (`'deposit'`, `'withdraw'`, `'transfer_in'`, `'transfer_out'`, `'card_debit'`, etc.) |

## Returns

Array of raw `pc_banking_transactions` rows ordered newest-first. Returns `{}` for unknown accountId.

## Example

```lua
local lastWeek = exports['pc-banking']:ExportAccountTransactions(42, {
    dateFrom = os.date('%Y-%m-%d 00:00:00', os.time() - 7 * 86400),
    type     = 'transfer_out',
    limit    = 50,
})

for _, tx in ipairs(lastWeek) do
    print(tx.created_at, tx.amount, tx.description)
end
```
