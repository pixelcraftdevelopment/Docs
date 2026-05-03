# Shop Locations

`Config.ShopLocations` defines every physical shop on the map. Each shop is a distinct entry with its own type, jobs, mods, tuning, locations, and (optionally) repair zones, parts shops, stashes, and dyno station.

## Shop Types

```lua
type = "self-service" | "owned"
```

| Type | Behavior |
|------|----------|
| `self-service` | Anyone walking in can use the customization menu directly. No mechanic needed. |
| `owned` | Run by mechanics. Customers either get serviced by an on-duty mechanic, or self-service if shop allows it. |

## Schema

```lua
Config.ShopLocations = {
    bennys = {
        type             = "self-service",
        logo             = "bennys.png",
        label            = "Benny's Original Motor Works",
        allowSocietyPay  = true,
        allowFreeService = true,
        locations        = { --[[ array of location entries ]] },
        blip             = { --[[ blip styling table ]] },
        mods             = { --[[ per-category toggle + price ]] }
    },

    lscustoms = {
        type                        = "owned",
        job                         = "mechanic",
        label                       = "LS Customs",
        logo                        = "ls_customs.png",
        commission                  = 0,
        allowSocietyPay             = true,
        allowFreeService            = false,
        allowSelfServiceWhenOffDuty = true,
        selfServiceJobs             = { "police", "ambulance" },
        locations                   = { --[[ array of location entries ]] },
        blip                        = { --[[ blip styling ]] },
        repairZones                 = { --[[ keyed polygon zones ]] },
        mods                        = { --[[ per-category toggle + price ]] },
        tuning                      = { --[[ per-category toggle + item flags ]] },
        shops                       = { --[[ walk-up parts counters ]] },
        stashes                     = { --[[ job storage ]] },
        dynoStation                 = { coords = vector3(...), rotation = vector3(...) }
    }
}
```

## Top-Level Fields

| Field | Type | Purpose |
|-------|------|---------|
| `type` | string | `"self-service"` or `"owned"` |
| `label` | string | Display name in UI and target prompts |
| `logo` | string | Logo asset filename for the UI |
| `job` | string (optional) | If set, this job is the only one that can be a mechanic at this shop. Overrides `Config.MechanicJobs` for this shop only |
| `allowSocietyPay` | boolean | Whether society funds can be used to pay invoices at this shop |
| `allowFreeService` | boolean | Whether the shop allows waiving the bill (gated by role's `allowFreeService` too) |
| `commission` | number | Owned shops only — commission rate on services (0 = none) |
| `allowSelfServiceWhenOffDuty` | boolean | Owned shops only — allow customers to self-service when no mechanic is on duty |
| `selfServiceJobs` | table | Owned shops only — jobs allowed to self-service even when employees are on duty (police, ambulance, etc.) |

## Locations

A shop can have multiple locations (the LS Customs entry has two — main entrance and back-room employee area):

```lua
locations = {
    { coords = vector3(-337.25, -137.2, 38.35), size = 6.5, showBlip = true,  employeeOnly = false, allowSelfService = true  },
    { coords = vector3(-324.2,  -132.0, 38.54), size = 3.0, showBlip = false, employeeOnly = true,  allowSelfService = false }
}
```

### Location Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `coords` | vector3 | World position of the interaction point |
| `size` | number | Radius (m) of the interaction zone. Drives target prompt range and trigger detection |
| `showBlip` | boolean | Whether this specific location renders a map blip. The shop's `blip` table provides the styling |
| `employeeOnly` | boolean | If true, only shop employees (matching the shop's `job` field or `Config.MechanicJobs`) can interact here |
| `allowSelfService` | boolean | Owned shops only — if true, non-employees can open the customization menu at this point. Combines with the shop-level `allowSelfServiceWhenOffDuty` and `selfServiceJobs` |

### Locations × Self-Service Logic

For owned shops, whether a customer can self-service at a given location is the AND of:

```
location.allowSelfService = true
AND (
    no mechanic on duty AND shop.allowSelfServiceWhenOffDuty = true
    OR
    customer's job is in shop.selfServiceJobs
)
AND
location.employeeOnly = false
```

So an `employeeOnly = true` location is locked even if the shop is otherwise self-service-friendly — typical for back-room or staff-only entry points.

## Blips

```lua
blip = { id = 446, color = 47, scale = 0.7, visibleToAll = true }
```

### Blip Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `id` | number | GTA blip sprite ID. `446` = wrench icon, `402` = paint brush, `527` = LS Customs, `72` = vehicle. See FiveM blip sprite reference for the full list |
| `color` | number | GTA blip colour ID. `47` = orange, `2` = green, `3` = blue, `1` = red, etc. |
| `scale` | number | Blip size multiplier. `0.7` = slightly smaller than default, `1.0` = default, `1.5` = noticeably larger |
| `visibleToAll` | boolean (optional) | If `false` or omitted, blip is only visible to players whose framework job matches the shop's `job` field (used for the police garage so only cops see it). If `true`, all players see it |

Each location with `showBlip = true` uses this same blip styling — there's no per-location blip overrides. If you need different blip colours per location, split into separate shop entries.

## Mods

Per-shop toggle and pricing for each mod category:

```lua
mods = {
    repair           = { enabled = true,  price = 1500, vehiclevaluePortion = 0.01 },
    performance      = { enabled = true,  price = 8000, vehiclevaluePortion = 0.01, multiplier = 0.15 },
    cosmetics        = { enabled = true,  price = 7500, vehiclevaluePortion = 0.01, multiplier = 0.12 },
    stance           = { enabled = true,  price = 4000, vehiclevaluePortion = 0.01 },
    respray          = { enabled = true,  price = 3500, vehiclevaluePortion = 0.01 },
    wheels           = { enabled = true,  price = 5000, vehiclevaluePortion = 0.01, multiplier = 0.18 },
    neonLights       = { enabled = true,  price = 2500, vehiclevaluePortion = 0.01 },
    headlights       = { enabled = true,  price = 1800, vehiclevaluePortion = 0.01 },
    tyreSmoke        = { enabled = true,  price = 2000, vehiclevaluePortion = 0.01 },
    bulletproofTyres = { enabled = true,  price = 6000, vehiclevaluePortion = 0.01 },
    extras           = { enabled = true,  price = 2500, vehiclevaluePortion = 0.01 }
}
```

### Mod Category Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `enabled` | boolean | Whether the category is offered at this shop. If false, the category is hidden from the customization menu at this shop |
| `price` | number | Base price for the category |
| `vehiclevaluePortion` | number | Fraction of vehicle value added on top of base price (default 0.01 = 1% of vehicle value). Ignored when `Config.VehcilePricingInParts = false` |
| `multiplier` | number (optional) | Additional multiplier on top of base + value. Present on `performance` (0.15), `cosmetics` (0.12), and `wheels` (0.18) by default to make them scale more aggressively with vehicle value |

### Pricing Interaction

Final installation price for a category at a shop is computed as:

```
final = (price + vehicleValue × vehiclevaluePortion) × (multiplier if present)
```

The pricing engine (`Config.AlwaysProfit`, `Config.ProfitMargin`, `Config.MinimumProfitBuffer`, `Config.UseLowestShopPrice`) then layers on top to enforce profit floors and cross-shop price selection. See [Pricing Engine](pricing.md) for the full chain.

### Shop Mods × Repair Zones × Roles

Three layers gate whether a category can actually be performed at a given moment:

1. **Shop level** — `mods[category].enabled` must be `true` here
2. **Repair zone** — if `Config.RepairZones.enabled` and the mechanic is inside a zone, the zone's `allowedMods` whitelist must include the category (or be empty)
3. **Role** — the mechanic's role permissions must include `canInstallParts` (and `canApplyTuning` for tuning, `canInstallNitrous` for nitrous)

All three must allow. The repair zone failure is the one that visually flashes to the player (configurable via `Config.RepairZones.flashZoneOnRestriction`).

## Tuning (owned shops only)

```lua
tuning = {
    engines       = { enabled = true, needsItem = true,  requiresPayment = false },
    drivetrains   = { enabled = true, needsItem = true,  requiresPayment = false },
    tyres         = { enabled = true, needsItem = true,  requiresPayment = false },
    brakes        = { enabled = true, needsItem = true,  requiresPayment = false },
    driftTuning   = { enabled = true, needsItem = true,  requiresPayment = false },
    antiRollBars  = { enabled = true, needsItem = true,  requiresPayment = false },
    launchControl = { enabled = true, needsItem = false, requiresPayment = false }
}
```

### Tuning Category Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `enabled` | boolean | Whether this tuning category is offered at this shop. If false, the category is hidden from the tuning menu here |
| `needsItem` | boolean | Whether installation consumes a physical item from inventory. When true, the item key from `Config.Tuning[category][option].itemName` must be in inventory |
| `requiresPayment` | boolean | Whether a separate cash payment is taken on top of the item cost. When false, having the item is sufficient (the item itself was the cost) |

### Tuning Interaction

The actual tuning options (I4 engine, V8, slick tyres, etc.) are defined in `Config.Tuning` (see [Tuning](tuning.md)). The shop block here only decides:

- Whether the category appears at this shop (`enabled`)
- Whether the part item is consumed on install (`needsItem`)
- Whether an extra cash transaction happens (`requiresPayment`)

A shop with `tuning.engines = { enabled = true, needsItem = true, requiresPayment = false }` lets mechanics install engines using the `i4_engine`/`v6_engine`/etc. items in inventory, with no extra cash bill. Setting `requiresPayment = true` adds a service-fee transaction on top.

`launchControl` ships with `needsItem = false` because launch control doesn't have a physical part — it's purely a software/tuning toggle.

## Walk-Up Parts Shops

Owned shops can have one or more in-shop parts shops (a ped or marker that opens a buy menu):

```lua
shops = {
    {
        name     = "Servicing Supplies",
        coords   = vector3(-345.44, -131.22, 38.04),
        size     = 1.0,
        usePed   = false,
        pedModel = "s_m_m_gaffer_01",
        marker   = {
            id            = 23,
            size          = { x = 1.0, y = 1.0, z = -0.1 },
            color         = { r = 255, g = 255, b = 255, a = 80 },
            bobUpAndDown  = 0,
            faceCamera    = 0,
            rotate        = 1,
            drawOnEnts    = 0
        },
        items = {
            { name = "engine_oil",       label = "Engine Oil",       price = 35 },
            { name = "spark_plug",       label = "Spark Plug",       price = 55 },
            { name = "tyre_replacement", label = "Tyre Replacement", price = 1200 }
        }
    }
}
```

### Walk-Up Shop Fields

| Field | Type | Purpose |
|-------|------|---------|
| `name` | string | Display name shown in target prompt and shop UI title |
| `coords` | vector3 | World position of the counter |
| `size` | number | Interaction radius. Also used as marker draw radius |
| `usePed` | boolean | If true, spawn a ped at `coords` using `pedModel`. If false, draw a marker only |
| `pedModel` | string | Ped model hash name (e.g. `"s_m_m_gaffer_01"`). Ignored when `usePed = false` |
| `marker` | table | Marker definition. Used when `usePed = false`, or as the floor pad under a ped |
| `items` | table | Array of items sold at this counter |

### Marker Sub-Fields

Standard FiveM marker parameters. Each marker entry uses:

| Field | Type | Purpose |
|-------|------|---------|
| `id` | number | GTA marker type (`23` = filled circle on ground, `1` = vertical cylinder, `2` = downward arrow, etc.) |
| `size` | table | `{ x, y, z }` scale of the marker. Negative `z` flattens it onto the floor |
| `color` | table | `{ r, g, b, a }` 0-255. `a` (alpha) controls transparency |
| `bobUpAndDown` | 0 or 1 | Whether the marker bobs (1) or stays still (0) |
| `faceCamera` | 0 or 1 | Whether the marker rotates to face the player camera |
| `rotate` | 0 or 1 | Whether the marker spins on its Z axis |
| `drawOnEnts` | 0 or 1 | Whether the marker renders on top of vehicles/entities passing through |

### `items[]` Sub-Fields

Each entry inside the `items` array represents a single counter SKU:

| Field | Type | Purpose |
|-------|------|---------|
| `name` | string | Inventory item key. Must exist in your inventory resource's items list |
| `label` | string | Display name shown in the buy menu |
| `price` | number | On-counter unit price |

`items[].price` is the **on-counter** price paid by mechanics buying parts for an immediate job. It is independent of `Config.Shop.Items[item].price`, which is the **delivery / restock** price used by the central catalogue. The same item key can have different prices in each context.

Counter items don't track stock — they're treated as always-available. Stock tracking only applies to the central catalogue.

## Stashes

Owned shops can have one or more stashes (job storage):

```lua
stashes = {
    {
        name     = "Parts Bin",
        coords   = vector3(-339.24, -132.2, 38.02),
        size     = 1.0,
        usePed   = false,
        pedModel = "s_m_m_gaffer_01",
        marker   = {
            id            = 23,
            size          = { x = 1.0, y = 1.0, z = -0.1 },
            color         = { r = 255, g = 255, b = 255, a = 80 },
            bobUpAndDown  = 0,
            faceCamera    = 0,
            rotate        = 1,
            drawOnEnts    = 0
        },
        slots  = 10,
        weight = 50000
    }
}
```

### Stash Fields

| Field | Type | Purpose |
|-------|------|---------|
| `name` | string | Stash display name. Also forms the stash identifier inside the inventory resource |
| `coords` | vector3 | World position of the stash interact point |
| `size` | number | Interaction radius |
| `usePed` | boolean | If true, spawn a ped (e.g. a clerk). If false, marker-only |
| `pedModel` | string | Ped model. Ignored when `usePed = false` |
| `marker` | table | Marker definition. Same sub-fields as walk-up shop markers |
| `slots` | number | Stash slot count |
| `weight` | number | Stash weight cap (grams). Used by inventory systems that track weight |

Stashes register with the detected inventory system using shop-keyed identifiers — each shop's stash gets its own storage scope, so two shops with stashes named `"Parts Bin"` don't share contents.

### Interaction with Roles

Stash access is gated by the inventory resource's stash permissions, typically driven by the framework job. The shop's `job` field decides which job has access. Internal role permissions (`Config.Roles[role].permissions`) do not gate stash access directly — every employee on the shop's job can use the stash unless your inventory resource adds extra rules.

## Repair Zones

Optional polygon zones inside the shop. See [Repair Zones](repair-zones.md) for the full schema.

## Dyno Station

```lua
dynoStation = {
    coords   = vector3(-326.7, -137.66, 37.94),
    rotation = vector3(0.0, 0.0, 250.36)
}
```

### Dyno Station Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `coords` | vector3 | World position where the dyno platform props spawn |
| `rotation` | vector3 | `{ pitch, roll, heading }` orientation in degrees. `pitch` = X-axis tilt (rare), `roll` = Y-axis tilt (rare), `heading` = Z-axis rotation (the one that actually matters for facing direction) |

If `dynoStation` is omitted from a shop entry, no dyno spawns at that shop. Self-service shops typically omit it.

### Dyno Station × Global Dyno Settings

The `dynoStation` block only specifies **where** the platform spawns. Behaviour, alignment overlay sizing, DUI camera, and history all live in `Config.DynoHistory` and the `Config.Dyno*` settings in `config.lua`. See [Dyno](dyno.md) for the full set.

The platform won't spawn at all if `Config.EnableDynoPlatform = false`, regardless of how many shops have a `dynoStation` entry.

## Adding a New Shop

1. Add a new entry to `Config.ShopLocations` with a unique key.
2. Set `type`, `job` (if owned), `label`, `logo`, and `locations`.
3. Configure `mods` for which categories you want offered.
4. (Owned shops) configure `tuning`, `repairZones`, `shops`, `stashes`, and `dynoStation` as needed.
5. Restart `pc-mechanic`.
6. (Owned shops) use `/setowner` to assign an initial owner.
