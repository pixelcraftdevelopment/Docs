# GetPhoneSessionIdentifier

Returns the identifier currently logged into the phone app at a given src. Differs from the framework's player identifier in multi-character setups where a player can be using their second character's phone session.

```lua
local sessionIdent = exports['pc-banking-phone']:GetPhoneSessionIdentifier(src)
```

| Param | Type | Notes |
|-------|------|-------|
| `src` | number | Server src |

## Returns

* `string` — identifier of the active phone session
* `nil` — if no active phone session at that src

## Example

```lua
local who = exports['pc-banking-phone']:GetPhoneSessionIdentifier(src)
if who then
    -- safe to use 'who' for phone-context queries (mail, contacts, etc.)
end
```

## When To Use

Use this for any phone-context operation to avoid leaking data across multi-character logins. Direct framework identifier lookups bypass the phone session and can return the wrong character's data.
