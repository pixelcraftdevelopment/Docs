# IsCardFrozen

**Side:** Server

Check if a card is locked (player-locked OR admin-locked).

```lua
local locked = exports['pc-banking']:IsCardFrozen(cardNumber)
```

## Returns

* `true` if locked
* `false` if not locked
* `nil` if card not found

## Example

```lua
if exports['pc-banking']:IsCardFrozen(cardNumber) then
    return notify('Card is locked')
end
```
