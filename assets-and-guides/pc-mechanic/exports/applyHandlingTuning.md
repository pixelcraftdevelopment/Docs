# applyHandlingTuning

**Side:** Client

Applies a tuning configuration's resulting handling values to a vehicle entity. Internally combines tuning + servicing handling modifiers, then writes the result via the FiveM handling natives.

## Signature

```lua
exports['pc-mechanic']:applyHandlingTuning(vehicle, tuningConfig)
```

| Parameter | Type | Purpose |
|-----------|------|---------|
| `vehicle` | integer | Vehicle entity handle |
| `tuningConfig` | table | Same shape as [`getTuningHandlingModifiers`](getTuningHandlingModifiers.md) |

## Notes

- Network ownership applies — only the vehicle's owner sees the change reliably (use FiveM's owner migration patterns if you need a remote vehicle).
- Servicing modifiers are layered on top automatically based on the vehicle's current part health.
- Reapplied automatically when a player enters the vehicle (`pc-mechanic:cl:reapply-custom-visuals`).
