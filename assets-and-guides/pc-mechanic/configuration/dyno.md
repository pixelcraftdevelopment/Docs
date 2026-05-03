# Dyno

The dyno consists of a global block in `config.lua` (platform behavior, alignment, camera, history) and a per-shop coordinate in `Config.ShopLocations[shop].dynoStation` (where the platform spawns).

## Global Block

```lua
Config.EnableDynoPlatform = true
Config.ShowTabletDuringDyno = false
Config.EnableDynoAlignment = true

Config.DynoAlignLeft  = { offset = vector3(-0.85, -1.53, 0.0), size = vector3(0.14, 0.18, 0.0) }
Config.DynoAlignRight = { offset = vector3( 0.83, -1.52, 0.0), size = vector3(0.16, 0.17, 0.0) }
Config.DynoAlignHeadingTolerance = 10.0

Config.DynoScreenCamOffset      = vector3(0.95, 2.90, 1.85)
Config.DynoScreenLookAtOffset   = vector3(0.90, 6.25, 0.85)
Config.DynoScreenCamFov         = 68.5
Config.DynoScreenInteractDist   = 2.0

Config.DynoHistory = {
    enabled = true,
    limit   = 5
}
```

### Platform Toggles

| Field | Purpose |
|-------|---------|
| `EnableDynoPlatform` | Master switch for the dyno (props, DUI screen, alignment overlay, animations) |
| `ShowTabletDuringDyno` | Whether the tablet stays visible during a dyno test. Default `false` to keep the screen visible |
| `EnableDynoAlignment` | Show the wheel-alignment overlay when driving near a dyno platform |

### Alignment Indicators

`DynoAlignLeft` / `DynoAlignRight` define the two glowing rectangles that show where each front wheel needs to land:

- `offset` — relative to the dyno station coords (X, Y, Z)
- `size` — width, depth, (unused Z)

`DynoAlignHeadingTolerance` is the heading match window in degrees. Within tolerance the indicators are green, outside they're red.

Tweak these if your dyno prop has wheel rollers in different positions than the default.

### DUI Screen Camera

| Field | Purpose |
|-------|---------|
| `DynoScreenCamOffset` | Camera position relative to dyno station |
| `DynoScreenLookAtOffset` | Where the camera looks |
| `DynoScreenCamFov` | Field of view |
| `DynoScreenInteractDist` | Distance from screen to allow interaction |

These control the cinematic camera angle when watching a dyno run. Adjust for custom dyno props or alternate room layouts.

### Per-Plate History

```lua
Config.DynoHistory = {
    enabled = true,
    limit   = 5
}
```

| Field | Purpose |
|-------|---------|
| `enabled` | Whether dyno test results are persisted |
| `limit` | Max entries returned per plate (newest kept, oldest dropped) |

History persists in MySQL via oxmysql. Setting `enabled = false` disables persistence — runs still work, just nothing is saved.

## Per-Shop Placement

```lua
dynoStation = {
    coords   = vector3(-326.7, -137.66, 37.94),
    rotation = vector3(0.0, 0.0, 250.36)    -- pitch, roll, heading
}
```

| Field | Purpose |
|-------|---------|
| `coords` | World position where platform props spawn |
| `rotation` | Orientation. Z is heading; X and Y rarely change unless your dyno is on an incline |

Add `dynoStation` to any owned shop entry to give it a dyno. Self-service shops (Benny's, LSPD garage) don't get one by default; you can add one if you want them to.

## Dyno as Inspection

The dyno is also wired as an inspection minigame in `Inspection.lua`:

```lua
dynoinspection = {
    parts      = { "suspension", "brakePads" },
    label      = "Dyno Inspection",
    needsItem  = true,
    itemNeeded = "dyno_access",
    itemLabel  = "Dyno Access",
    prop       = "dynoinspection"
}
```

Inspecting via the dyno requires the `dyno_access` item. The same access doubles as the test "ticket" — you need the item to either run a power test or an inspection.

Unlike the other inspection minigames, dyno inspection doesn't have variants or difficulty options — it uses the dyno run itself.

## Dependencies

- `pc-mechanic-props` must be running (provides the dyno platform model)
- `oxmysql` must be running for history persistence
