# Tuning

`pc-mechanic/config/Tuning.lua` defines the seven tuning categories: engines, anti-roll bars, tyres, brakes, launch control, drivetrains, drift tuning.

## Schema

```lua
Config.Tuning = {
    engines = {
        categoryLabel = "Engines",
        [1] = {
            name               = "I4 Turbo 2.5L",
            icon               = "Droplets",
            description        = "Twin-turbo charged 2.5L engine with strong mid-range power.",
            specs              = { displacement = "2500cc", maxPower = "320hp", maxTorque = "310lb-ft" },
            itemName           = "i4_engine",
            price              = 31500,
            gamecaraudio       = "sultan2",
            customHandlingData = true,
            sequencePriority   = 1,
            whitelist          = "combustion",
            handling = {
                fInitialDriveForce            = 0.25,
                fDriveInertia                 = 1.0,
                fInitialDriveMaxFlatVel       = 130.0,
                fClutchChangeRateScaleUpShift = 4.0,
                fClutchChangeRateScaleDownShift = 3.0
            }
        }
        -- additional [2], [3], [4], [5] options follow
    }
    -- additional categories: antiRollBars, tyres, brakes, launchControl, drivetrains, driftTuning
}
```

## Category-Level Fields

| Field | Type | Purpose |
|-------|------|---------|
| `categoryLabel` | string | Display name for the category in the tuning menu (e.g. `"Engines"`, `"Drivetrains"`) |
| `[1]`, `[2]`, ... | table | Numeric-indexed table of options inside the category. Index order is display order |

## Per-Option Fields

| Field | Type | Purpose |
|-------|------|---------|
| `name` | string | Display name |
| `icon` | string | Lucide icon name (e.g. `"Droplets"`, `"Wind"`, `"Zap"`, `"Disc3"`, `"SlidersVertical"`, `"LoaderPinwheel"`, `"Gauge"`, `"Cog"`, `"ArrowLeftRight"`, `"Wrench"`) or custom path `"custom/file.png"` (placed in `web/dist/icons/tuning/`) |
| `description` | string | Free text shown on the tuning detail page |
| `specs` | table | Free-form spec sheet shown in UI. Each key/value pair becomes a row (label / value). Common keys: `displacement`, `maxPower`, `maxTorque`, `treadDepth`, `compound`, `gripRating`, `rotorSize`, `material`, `biteForce`, `barDiameter`, `rollReduction`, `powerSplit`, `differential`, `torqueDistribution`, `transferCase`, `steeringAngle`, `suspensionStiffness`, `powerOversteer`, `responseTime`, `tractionGain`, `optimalRPM`, `replacement`, `warranty`, `labor` |
| `itemName` | string | Inventory item required to install. Must match a key in `Config.Shop.Items` for restock orders to work, and a key in any walk-up shop's `items` for over-the-counter purchase |
| `price` | number | Installation price |
| `gamecaraudio` | string (optional) | When set, swaps the engine sound to another GTA model's audio (e.g. `"jugular"`, `"sultan2"`, `"comet4"`, `"schafter3"`). Only meaningful for engine swaps |
| `customHandlingData` | boolean | Whether the `handling` block actually applies. If `false`, only sound/cosmetic side applies — handling is untouched. Used by the Engine Replacement entry to avoid changing handling on a recovery |
| `sequencePriority` | number | Order of application when multiple tuning options stack on one vehicle. Lower priority applies first; higher priority overwrites overlapping handling values |
| `whitelist` | string \| boolean | `"combustion"` = combustion-only, `"electric"` = electric-only, `false` = unrestricted (used by Launch Control). Omitted = unrestricted |
| `blacklist` | table (optional) | Array of model names where this option is unavailable. Example: V12 ships with `blacklist = { "panto" }` so it can't go in a Panto |
| `requiresSeizedEngine` | boolean (optional) | When true, the option only appears if the vehicle's engine has seized. Used by the Engine Replacement entry as the recovery path |
| `handling` | table | Map of handling field name → numeric value. Applied to the vehicle's `CHandlingData` (or `CFlyingHandlingData`/`CBikeHandlingData`/`CBoatHandlingData` for non-cars) on install |

## Sequence Priorities (Defaults)

| Priority | Category |
|----------|----------|
| 1 | Engines |
| 2 | Tyres |
| 3 | Brakes |
| 4 | Drivetrains |
| 5 | Drift Tuning |
| 6 | Launch Control |
| 7 | Anti-Roll Bars |
| 10 | Engine Replacement |

When multiple tuning options are installed on a vehicle, handling values are layered in priority order. Higher priority overwrites earlier values — meaning a drift kit (priority 5) will override traction values set by tyres (priority 2). This is intentional: drift cars should feel like drift cars regardless of the tyres.

## Handling Fields

The `handling` table accepts any field listed in `gameplaydata.lua → HANDLING_KEY_CLASS_MAP`. The most useful ones for cars:

| Field | What it controls |
|-------|------------------|
| `fInitialDriveForce` | Engine power output multiplier |
| `fInitialDriveMaxFlatVel` | Top speed |
| `fDriveInertia` | Engine response to throttle |
| `fClutchChangeRateScaleUpShift` / `DownShift` | Shift speed |
| `fBrakeForce` | Brake strength |
| `fSteeringLock` | Max steering angle in degrees |
| `fTractionCurveMin` / `Max` / `Lateral` | Tyre grip curves |
| `fTractionLossMult` | Multiplier for traction loss in low-grip scenarios |
| `fLowSpeedTractionLossMult` | Wheelspin behaviour at low speed (negative = anti-spin) |
| `fAntiRollBarForce` | Roll stiffness |
| `fDriveBiasFront` | 0 = RWD, 0.5 = AWD, 1.0 = FWD |
| `fInitialDragCoeff` | Aero drag |

For motorcycles, planes, and boats, additional fields apply (see `gameplaydata.lua` for the full classification).

## Game Car Audio

`gamecaraudio` sets the engine sound by referencing another vehicle's audio bank. Common picks:

- `sultan2` — high-revving I4 turbo
- `comet4` — refined V6
- `jugular` — V8 with backfires and crackle
- `schafter3` — V12 grunt

Any vehicle audio name works — match the engine character to the swap.

## Engine Replacement Special Case

```lua
[5] = {
    name = "Engine Replacement",
    icon = "Wrench",
    itemName = "engine_replacement",
    price = 157500,
    customHandlingData = false,         -- doesn't change handling — restoration only
    sequencePriority = 10,              -- applies last to overwrite prior damage states
    whitelist = "combustion",
    handling = {},
    requiresSeizedEngine = true         -- only available on a seized engine
}
```

This is the recovery path for engine seizure. Unlike other engine entries, it doesn't change the spec — it restores the vehicle to working order, clearing damage flags. Without this entry, a seized engine has no recovery mechanism.

## Whitelist / Blacklist Behaviour

| `whitelist` value | Effect |
|-------------------|--------|
| `"combustion"` | Only available on combustion vehicles |
| `"electric"` | Only available on electric vehicles |
| `false` | Available on all vehicles (used by Launch Control) |
| (omitted) | Available on all vehicles |

`blacklist = { "model1", "model2" }` blocks the option on specific models regardless of the whitelist. Useful for plausibility — V12 in a small hatchback isn't credible.

## Stock Linkage

`itemName` must match a key in:

- `Config.Shop.Items` (central catalogue) — for restock orders
- `Config.ShopLocations[shop].shops[].items` (walk-up) — for buy-now

If the item isn't anywhere, the tuning option exists but no one can buy the part to install it.
