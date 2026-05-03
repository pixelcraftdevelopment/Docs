# setmods

**Side:** Client

Applies a properties table onto a vehicle entity. Accepts the same shape returned by [`getmods`](getmods.md). Used by garage systems, tuner saves, and persistence integrations.

## Signature

```lua
exports['pc-mechanic']:setmods(vehicle, props, withStatebags)
```

| Parameter | Type | Purpose |
|-----------|------|---------|
| `vehicle` | integer | Vehicle entity handle |
| `props` | table | Properties table (from `getmods` or DB) |
| `withStatebags` | boolean (optional) | When true, also write pc-mechanic statebag fields (stance, tuning, servicing, etc.) |

## Returns

`boolean` — `true` if applied, `false` on bad input or non-network owner.

## Notes

- For network-controlled vehicles, the caller must own the entity (or the call no-ops on non-networked entities).
- When `withStatebags` is omitted/false, only the native vehicle props are written; statebag-driven systems remain untouched.

## Example

```lua
local props = MySQL.scalar.await('SELECT vehicle FROM player_vehicles WHERE plate = ?', { plate })
exports['pc-mechanic']:setmods(vehicle, json.decode(props), true)
```
