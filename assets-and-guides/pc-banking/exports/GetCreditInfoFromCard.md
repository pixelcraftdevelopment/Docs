# GetCreditInfoFromCard

Credit-card-only export. Returns `nil` for debit cards.

```lua
local info = exports['pc-banking']:GetCreditInfoFromCard(cardNumber)
```

## Returns

```lua
{
    creditLimit   = 50000,
    creditBalance = 12000,    -- amount charged (currently owed)
    available     = 38000,    -- limit - balance
    isFrozen      = false,
}
```

`nil` if card not found OR card is not a credit card.

## Example

```lua
local credit = exports['pc-banking']:GetCreditInfoFromCard(cardNumber)
if credit and credit.available >= amount then
    -- pre-auth check passed
end
```
