# IsAccountFrozen

**Side:** Server

Check if an account is currently frozen.

```lua
local frozen = exports['pc-banking']:IsAccountFrozen(accountId)
```

## Returns

* `true` if frozen
* `false` if not frozen
* `false` for non-existent accountId

## Example

```lua
if exports['pc-banking']:IsAccountFrozen(accountId) then
    return notify('Cannot process — account locked')
end
```
