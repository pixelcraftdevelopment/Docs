# getServicingHandlingModifiers

**Side:** Client

Computes the resulting handling table after part-degradation effects are applied. Worn suspension reduces stiffness, worn tyres reduce traction curves, worn brakes reduce brake force, and so on (see [Servicing Guide](../guide/servicing.md) for the per-part effect list).

## Signature

```lua
exports['pc-mechanic']:getServicingHandlingModifiers(vehicle, handling, servicingHealth)
```

| Parameter | Type | Purpose |
|-----------|------|---------|
| `vehicle` | integer | Vehicle entity handle (used to detect electric/combustion type) |
| `handling` | table | Base handling table to apply degradation onto |
| `servicingHealth` | table | Per-part health map (`{ engineOil = 75, tyres = 40, ... }`) |

## Returns

`table` — new handling table reflecting the wear-driven reductions.

## Notes

- The vehicle handle decides which set of parts is relevant (combustion vs electric — see `Config.Servicing` whitelists).
- Pure computation; does not modify the vehicle.
- Pair with [`getTuningHandlingModifiers`](getTuningHandlingModifiers.md) for "what would this car drive like at X tuning + Y wear" previews.
