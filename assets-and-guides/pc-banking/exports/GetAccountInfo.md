# GetAccountInfo

Fetch a single account by DB id.

```lua
local acc = exports['pc-banking']:GetAccountInfo(accountId)
```

## Returns

```lua
{
    id              = 42,
    ownerIdentifier = 'ABC123',
    bankName        = 'fleeca',
    accountType     = 'checking_fleeca',
    accountNumber   = 'FL00000142',
    balance         = 12345,
    accountClass    = 'personal',
    isPrimary       = true,
    isFrozen        = false,
    frozenBy        = nil,
    freezeReason    = nil,
}
```

`nil` if account not found.

## Example

```lua
local acc = exports['pc-banking']:GetAccountInfo(42)
if acc then print(acc.ownerIdentifier, acc.balance) end
```
