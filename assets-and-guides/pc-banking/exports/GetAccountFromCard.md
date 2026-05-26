# GetAccountFromCard

**Side:** Server

Resolve a card number to its linked account.

```lua
local info = exports['pc-banking']:GetAccountFromCard(cardNumber)
```

## Returns

```lua
{
    accountId       = 42,
    accountNumber   = 'FL00000042',
    balance         = 12345,
    ownerIdentifier = 'ABC123',
    bankName        = 'fleeca',
    isFrozen        = false,
}
```

`nil` if card or linked account is not found.

## Example

```lua
local info = exports['pc-banking']:GetAccountFromCard('4929123412341234')
if info and not info.isFrozen then
    print('Card belongs to', info.ownerIdentifier, '- balance', info.balance)
end
```
