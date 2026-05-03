# Mileage

Top-level config block in `pc-mechanic/config/config.lua`. Drives the entire passive servicing system.

## Settings

```lua
Config.MileageEnabled       = true
Config.MileageDisplay       = true
Config.MileageDisplayPosition = "bottom-right"
Config.MileageDisplayScale  = 1.0
Config.MileageUnit          = "kilometers"
Config.MileageUpdateKm      = 3
Config.MileageMultiplier    = 1
Config.AutoPurgeNonOwnedVehicles = true
```

| Field | Type | Purpose |
|-------|------|---------|
| `MileageEnabled` | boolean | Master switch for mileage tracking. If false, no part wears with distance — only damage-based wear applies |
| `MileageDisplay` | boolean | Show the HUD odometer in vehicle |
| `MileageDisplayPosition` | string | `"bottom-right"`, `"bottom-left"`, `"top-right"`, `"top-left"`, `"bottom-center"`, `"top-center"` |
| `MileageDisplayScale` | number | HUD size multiplier. 0.5 = half, 1.0 = default, 2.0 = double |
| `MileageUnit` | string | `"kilometers"` or `"miles"` — purely display |
| `MileageUpdateKm` | number | HUD only refreshes after this much new distance (km). Default 3 prevents flicker |
| `MileageMultiplier` | number | Multiplier on accumulation. 1 = realistic, 5 = 5× faster |
| `AutoPurgeNonOwnedVehicles` | boolean | If true, mileage data is wiped for non-owned vehicles (NPC traffic, mission cars, etc.) |

## Interactions

### With Servicing

Every part in `Config.Servicing` (in `Inspection.lua`) has a `durabilityKm` — the distance at which the part hits 0%. Mileage and durability work together:

```
condition % = max(0, 100 × (1 - kmDriven / durabilityKm))
```

`MileageMultiplier` scales `kmDriven` by speeding up accumulation. Setting it to 5 means a 100 km tyre lasts 20 in-world km before reaching 0%.

### With the Inspection Validity Threshold

```lua
Config.InspectionMileageThresholdPercent = 20
```

Inspections expire after a 20% mileage gain. With `MileageMultiplier = 5`, that 20% threshold is hit faster too — the multiplier compounds.

### With Damage-Based Wear

Mileage-based wear and damage-based wear are **additive**. A part can wear from both sources in the same trip — driving 50 km and then crashing degrades both quietly and visibly.

When `MileageEnabled = false`, only damage-based wear applies. Useful for casual servers that don't want maintenance pressure but still want crashes to matter.

## Recommended Tuning

| Server feel | `MileageMultiplier` | `MileageUpdateKm` |
|-------------|---------------------|-------------------|
| Hardcore RP | 1 | 1 |
| Standard RP | 3-5 | 3 |
| Casual / racing | 8-15 | 5 |
| Mileage off | n/a (`MileageEnabled = false`) | n/a |
