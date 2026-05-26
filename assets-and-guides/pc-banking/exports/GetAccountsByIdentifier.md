# GetAccountsByIdentifier

**Side:** Server

All accounts owned by a player. Excludes shared/business accounts the player is a member of (use [`GetAllBankingInfo`](GetAllBankingInfo.md) for that).

```lua
local accounts = exports['pc-banking']:GetAccountsByIdentifier(identifier)
```

## Returns

Array of account-info tables, ordered: primary first, then by `created_at` ascending.

```lua
{
    {
        id            = 42,
        bankName      = 'fleeca',
        accountType   = 'checking_fleeca',
        accountNumber = 'FL00000042',
        balance       = 12345,
        accountClass  = 'personal',
        isPrimary     = true,
        isFrozen      = false,
    },
    -- ...
}
```

Returns `{}` for unknown identifier.

## Example

```lua
for _, acc in ipairs(exports['pc-banking']:GetAccountsByIdentifier('ABC123')) do
    print(acc.bankName, acc.accountNumber, acc.balance)
end
```
