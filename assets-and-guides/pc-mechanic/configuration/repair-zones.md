# Repair Zones

Two layers of config: the **global** repair-zones behavior block in `config.lua`, and **per-shop** zone definitions inside each owned `Config.ShopLocations[shop].repairZones`.

## Global Block

```lua
Config.RepairZones = {
    enabled              = true,
    autoAdjust           = true,
    fallbackThickness    = 6.0,
    showZoneInfo         = true,
    flashZoneOnRestriction = true,
    flashDuration        = 3000,
    flashColor           = { r = 255, g = 50, b = 50, a = 120 }
}
```

| Field | Type | Purpose |
|-------|------|---------|
| `enabled` | boolean | Master switch. If false, no zone restriction at any shop |
| `autoAdjust` | boolean | Auto-snap polygon points to ground via raycast and detect ceiling height — works inside MLOs |
| `fallbackThickness` | number | Vertical extent used when ceiling detection fails (typical for outdoor zones with open sky) |
| `showZoneInfo` | boolean | Show a top-right panel with zone name and allowed mods when an employee enters/exits a zone |
| `flashZoneOnRestriction` | boolean | Briefly flash the nearest zone outline when a mechanic tries to work outside it |
| `flashDuration` | number | Flash duration in ms |
| `flashColor` | table | RGBA outline colour for the flash |

## Per-Shop Zones

Each owned shop can have any number of zones, keyed by a unique zone id:

```lua
repairZones = {
    main_garage = {
        label       = "Main Garage",
        points      = {
            vec3(-327.88, -133.89, 39.01),
            vec3(-326.41, -129.81, 39.01),
            vec3(-320.51, -131.25, 38.98),
            vec3(-321.8,  -135.7,  39.01)
        },
        thickness   = 8.0,
        allowedMods = {}
    },
    paint_bay = {
        label       = "Paint Bay",
        points      = { vec3(...), vec3(...), vec3(...), vec3(...) },
        thickness   = 6.0,
        allowedMods = { "respray" }
    }
}
```

### Zone Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| (zone key) | string | Unique zone id (e.g. `main_garage`, `paint_bay`). Used internally to identify the zone for flash and panel rendering |
| `label` | string | Display name shown in the top-right in-zone info panel when an employee enters |
| `points` | table | Array of `vec3(x, y, z)` polygon corners. Order them clockwise or counter-clockwise around the perimeter — the system closes the loop automatically. Z values are raycast-snapped to ground if `Config.RepairZones.autoAdjust = true` |
| `thickness` | number | Vertical extent in metres. Caps at detected ceiling when `autoAdjust = true` and a ceiling is found inside an MLO |
| `allowedMods` | table | Whitelist of mod and tuning category keys allowed in this zone. Empty `{}` = all categories allowed |

### Polygon Notes

- A zone needs **at least 3 points** to form a polygon. Practical zones use 4–8 points
- Points sit on the floor plane; the zone extrudes upward by `thickness` to form a 3D volume
- The polygon does not need to be convex — concave shapes are accepted
- Reusing point lists across shops works, but each shop's `autoAdjust` ground-snap may produce different Z values

## Allowed Mod Keys

| Mods | Tuning |
|------|--------|
| `repair` | `engines` |
| `performance` | `drivetrains` |
| `cosmetics` | `tyres` |
| `stance` | `brakes` |
| `respray` | `driftTuning` |
| `wheels` | `antiRollBars` |
| `neonLights` | `launchControl` |
| `headlights` | |
| `tyreSmoke` | |
| `bulletproofTyres` | |
| `extras` | |

## How Zones Interact With Mod & Tuning Toggles

Three layers gate whether a category can be performed:

1. **Shop-level toggle** — `mods[category].enabled` and `tuning[category].enabled`
2. **Repair zone whitelist** — `repairZones[zone].allowedMods` (if non-empty)
3. **Role permission** — `canInstallParts` / `canApplyTuning` / etc.

All three must allow the action. The flash visualization fires on layer 2 — when the action is otherwise allowed but the mechanic is in the wrong zone (or no zone).

## Auto-Adjust Behavior

When `autoAdjust = true`:

- Each point's Z is raycast to the nearest ground hit. If you write `vec3(x, y, 39.01)` inside an MLO with floor at 38.98, the system snaps to 38.98 automatically.
- A ceiling raycast above the polygon's centre detects MLO ceilings; the zone's vertical extent caps at the detected ceiling height. If no hit (open sky), `fallbackThickness` is used.

This makes it possible to reuse the same point list across multiple shops with minor floor variation.

## Visualizing While Configuring

Use the admin command `/viewzones` (configurable name) at an owned shop to draw all the zones in 3D. Useful when authoring points for a custom MLO.
