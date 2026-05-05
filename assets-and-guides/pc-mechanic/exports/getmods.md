# getmods

**Side:** Client

Returns a complete vehicle properties table for the given entity. Combines the framework's native vehicle props (paint, mods, plate, etc.) with PC-Mechanic's extended fields.

## Signature

```lua
exports['pc-mechanic']:getmods(vehicle)
```

| Parameter | Type | Purpose |
|-----------|------|---------|
| `vehicle` | integer | Vehicle entity handle |

## Returns

`table | false` — properties table, or `false` if entity doesn't exist. Contains all framework-native vehicle props plus PC-Mechanic extended data.

## Example

```lua
local props = exports['pc-mechanic']:getmods(vehicle)
if props then
    print(json.encode(props))
end
```

## Pairs With

- [`setmods`](setmods.md) — write the same shape back onto a vehicle
- [`SaveVehicleProperties`](SaveVehicleProperties.md) — save the current props to the framework DB
