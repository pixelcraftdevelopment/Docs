# getTuningHandlingModifiers

**Side:** Client

Computes the resulting handling table after a tuning configuration is applied to a base handling table. Returns a *new* handling table — does not mutate the input.

## Signature

```lua
exports['pc-mechanic']:getTuningHandlingModifiers(handling, tuningConfig)
```

| Parameter | Type | Purpose |
|-----------|------|---------|
| `handling` | table | Base handling table (typically the vehicle's stock values) |
| `tuningConfig` | table | Tuning category → option key map |

### `tuningConfig` Shape

| Key | Type | Purpose |
|-----|------|---------|
| `engines` | string | Selected engine option key |
| `drivetrains` | string | Selected drivetrain option key |
| `turbocharging` | string | Turbo on/off |
| `tyres` | string | Selected tyre option key |
| `brakes` | string | Selected brake option key |
| `gearboxes` | string | Selected gearbox option key (if defined) |

## Returns

`table` — new handling table with each tuning option's `handling` block layered in `sequencePriority` order (lower priority first; higher priority overwrites overlapping fields).

## Notes

- Pure computation — does not touch any vehicle entity.
- Useful for previewing handling deltas in a custom UI without committing the change.

## Pairs With

[`applyHandlingTuning`](applyHandlingTuning.md) — actually apply the handling to a vehicle.
