# Servicing & Inspection

`pc-mechanic/config/Inspection.lua` defines serviceable parts, inspection minigames, and validity rules.

## Serviceable Parts

```lua
Config.Servicing = {
    -- Universal
    suspension = { enabled = true, durabilityKm = 1000, itemName = "suspension_parts",     itemLabel = "Suspension Parts",     itemQuantity = 1 },
    tyres      = { enabled = true, durabilityKm = 250,  itemName = "tyre_replacement",     itemLabel = "Tyre Replacement",     itemQuantity = 4 },
    brakePads  = { enabled = true, durabilityKm = 500,  itemName = "brakepad_replacement", itemLabel = "Brakepad Replacement", itemQuantity = 4 },

    -- Combustion only
    engineOil  = { enabled = true, durabilityKm = 100, itemName = "engine_oil",         itemLabel = "Engine Oil",         itemQuantity = 1, whitelist = "combustion" },
    clutch     = { enabled = true, durabilityKm = 500, itemName = "clutch_replacement", itemLabel = "Clutch Replacement", itemQuantity = 1, whitelist = "combustion" },
    airFilter  = { enabled = true, durabilityKm = 250, itemName = "air_filter",         itemLabel = "Air Filter",         itemQuantity = 1, whitelist = "combustion" },
    sparkPlugs = { enabled = true, durabilityKm = 150, itemName = "spark_plug",         itemLabel = "Spark Plug",         itemQuantity = 4, whitelist = "combustion" },

    -- Electric only
    evMotor    = { enabled = true, electric = true, durabilityKm = 2000, itemName = "ev_motor",   itemLabel = "EV Motor",   itemQuantity = 1, whitelist = "electric" },
    evBattery  = { enabled = true, electric = true, durabilityKm = 500,  itemName = "ev_battery", itemLabel = "EV Battery", itemQuantity = 1, whitelist = "electric" },
    evCoolant  = { enabled = true, electric = true, durabilityKm = 250,  itemName = "ev_coolant", itemLabel = "EV Coolant", itemQuantity = 1, whitelist = "electric" }
}
```

| Field | Purpose |
|-------|---------|
| `enabled` | Whether the part is part of the servicing system at all |
| `durabilityKm` | Distance (km) at which the part hits 0% from mileage alone |
| `itemName` | Inventory item required to replace the part |
| `itemLabel` | Display name |
| `itemQuantity` | Number of items consumed per replacement (e.g. 4 for tyres, 1 for engine oil) |
| `whitelist` | `"combustion"` or `"electric"` — restricts to that vehicle type |
| `electric` | Convenience flag; same effect as whitelist for EV parts |

## Top-Level Servicing Toggles

```lua
Config.ServicingDegradation  = true      -- master switch for part degradation
Config.ServiceNotifyValue    = 20        -- notify driver when a part drops below 20%
```

## Inspection Minigames

```lua
Config.InspectionMinigames = {
    obd = {
        parts       = { "engineOil", "clutch", "evMotor" },
        label       = "OBD Diagnostics",
        needsItem   = true,
        itemNeeded  = "obd_scanner",
        itemLabel   = "OBD-II Scanner",
        prop        = "obd",
        useExternal = "default",
        variant     = "random",
        difficulty  = "medium"
    },
    treadtest = {
        parts       = { "tyres" },
        label       = "Tread Depth Test",
        needsItem   = true,
        itemNeeded  = "tread_gauge",
        itemLabel   = "Tread Depth Gauge",
        prop        = "treadtest",
        useExternal = "default",
        variant     = "random",
        difficulty  = "medium"
    },
    pressure = {
        parts       = { "airFilter", "evCoolant" },
        label       = "Pressure Test",
        needsItem   = true,
        itemNeeded  = "pressure_gauge",
        itemLabel   = "Pressure Gauge",
        prop        = "pressure",
        useExternal = "default",
        variant     = "random",
        difficulty  = "medium"
    },
    multimeter = {
        parts       = { "sparkPlugs", "evBattery" },
        label       = "Multimeter Test",
        needsItem   = true,
        itemNeeded  = "multimeter",
        itemLabel   = "Multimeter",
        prop        = "multimeter",
        useExternal = "default",
        variant     = "random",
        difficulty  = "medium"
    },
    dynoinspection = {
        parts      = { "suspension", "brakePads" },
        label      = "Dyno Inspection",
        needsItem  = true,
        itemNeeded = "dyno_access",
        itemLabel  = "Dyno Access",
        prop       = "dynoinspection"
    }
}
```

### Inspection Minigame Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `parts` | table | Array of `Config.Servicing` keys this minigame can inspect. Each key listed here gets a condition reading on a successful pass |
| `label` | string | Display name shown in the tablet inspection menu |
| `needsItem` | boolean | Whether the inspection requires an item in inventory |
| `itemNeeded` | string | Inventory item key required when `needsItem = true` |
| `itemLabel` | string | Display name of the required item, used in error messages and tooltips |
| `prop` | string | Prop key used during the animation. Resolved by `pc-mechanic-props` |
| `useExternal` | string | `"default"` defers to `Config.UseExternalMinigames`. `"yes"` forces external (`pc-mechanic-minigames`). `"no"` forces the internal fallback. Omitted on `dynoinspection` because the dyno doesn't have a swappable minigame |
| `variant` | string | `"random"` (the system picks per session) or a specific variant key. Omitted on `dynoinspection` |
| `difficulty` | string | `"easy"`, `"medium"`, `"hard"`. Difficulty changes timing windows or success thresholds inside the minigame. Omitted on `dynoinspection` |

## Variants per Minigame

| Minigame | Variants |
|----------|----------|
| OBD | `random`, `signalLock`, `handshake`, `faultMemory` |
| Tread Test | `random`, `treadMatch`, `depthTrace` |
| Pressure | `random`, `pump`, `lock` |
| Multimeter | `random`, `rangeStop`, `peakHold`, `polarity` |
| Dyno Inspection | (single variant, uses the dyno platform) |

## Default Minigame Coverage

| Minigame | Inspects |
|----------|----------|
| OBD | engineOil, clutch, evMotor |
| Tread Test | tyres |
| Pressure | airFilter, evCoolant |
| Multimeter | sparkPlugs, evBattery |
| Dyno Inspection | suspension, brakePads |

Note that OBD covers both combustion (engineOil, clutch) and electric (evMotor) parts — the same tool reads different sub-systems based on vehicle type. Same for pressure (airFilter / evCoolant) and multimeter (sparkPlugs / evBattery).

## Inspection Validity

```lua
Config.InspectionTimeThreshold       = 1 * 24 * 60 * 60   -- 1 day in seconds
Config.InspectionMileageThresholdPercent = 20             -- 20% mileage increase
```

An inspection result is valid until **whichever expires first**:

- The time threshold (default: 1 day after inspection)
- A mileage gain of 20% (default) since the inspection

Both timers count from the inspection moment for that specific plate. Driving extensively after an inspection invalidates it sooner than the time threshold.

## Interactions

### With Mileage

`durabilityKm` works against `Config.MileageMultiplier`. A 250-km tyre at 5× multiplier wears out in 50 in-world km. The validity threshold (`InspectionMileageThresholdPercent`) compounds — fast multipliers mean inspections expire on shorter trips.

### With Damage System

Each minigame inspects parts that are also in `Config.DamageBasedDegradation` (in `ServicingDamage.lua`). The damage system writes the same condition values that the inspection minigame reads. So a fresh inspection gives the up-to-the-second condition, including any damage-driven wear.

### With Repair Zones & Roles

Performing the inspection requires:
- The minigame's `itemNeeded` item in inventory (when `needsItem = true`)
- The role's `canInspectVehicles` permission (in `Config.Roles`)
- (If repair zones enabled) standing inside a zone where mod category isn't restricted away — inspection itself isn't a category in `allowedMods`, so any zone allows it; outside-zone inspection is gated by `Config.RepairZones.enabled`

### With Item-Removal Behavior

Inspection items (OBD scanner, multimeter, etc.) are **reusable** by default — they're not consumed on use. The replacement items (oil, tyres, plugs) are consumed in `itemQuantity` count per replacement.

## Disabling a Part

Set `enabled = false` on any entry to remove it from the servicing system entirely. The part is no longer tracked, never wears, and doesn't show up in inspections. Useful for casual servers that don't want clutch wear, for example.
