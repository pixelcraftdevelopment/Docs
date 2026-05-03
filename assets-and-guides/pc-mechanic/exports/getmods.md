# getmods

**Side:** Client

Returns a complete vehicle properties table for the given entity. Combines the framework's native vehicle props (paint, mods, plate, etc.) with PC-Mechanic's statebag fields (stance, lighting, tuning config, servicing data, nitrous).

## Signature

```lua
exports['pc-mechanic']:getmods(vehicle)
```

| Parameter | Type | Purpose |
|-----------|------|---------|
| `vehicle` | integer | Vehicle entity handle |

## Returns

`table | false` — properties table, or `false` if entity doesn't exist.

Combined keys include framework-native props plus the following PC-Mechanic statebag fields:

| Key | Purpose |
|-----|---------|
| `pearlescentcolor` | Pearl-disable flag |
| `stancingOption` | Stance enabled (boolean) |
| `wheelsAdjIndv` | Per-wheel adjustment mode |
| `defaultStance`, `stance` | Stance offsets |
| `lgcontinstal`, `lcXenons`, `conglowAngle`, `lcUnderglow` | Lighting controller fields |
| `tuneData` | Active tuning config |
| `servicingState` | Per-part servicing health |
| `nitrousInstalledBottles`, `nitrousFilledBottles`, `nitrousCapacity` | NOS state |

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
