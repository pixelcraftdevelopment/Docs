# GetVehicleMileage

**Side:** Client

Reads the live mileage value off a vehicle entity's statebag.

## Signature

```lua
exports['pc-mechanic']:GetVehicleMileage(vehicle)
```

| Parameter | Type | Purpose |
|-----------|------|---------|
| `vehicle` | integer | Vehicle entity handle |

## Returns

`number | false` — current mileage in the configured unit (`Config.MileageUnit`), or `false` if the entity is invalid or has no plate.

## Notes

- Only returns a meaningful value when `Config.MileageEnabled = true`. With the system disabled, you'll get `0`.
- The statebag is updated every `Config.MileageUpdateKm` km of travel — values are not millimetre-accurate.

## Pairs With

- [`GetMileageUnit`](GetMileageUnit.md) — read the configured unit string.
- [`GetMileage`](GetMileage.md) — server-side equivalent that takes a plate.
