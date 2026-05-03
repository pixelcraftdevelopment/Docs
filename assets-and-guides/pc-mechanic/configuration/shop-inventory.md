# Shop Inventory & Pricing

Defined in `pc-mechanic/config/Shops.lua` under `Config.Shop`. This is the **central** parts catalogue used by the shop ordering / restock / delivery system. It's separate from per-shop walk-up parts shops (which have their own `items` block under `Config.ShopLocations[shop].shops[]`).

## Top-Level Shop Settings

```lua
Config.Shop = {
    DeliveryTimeMinMinutes = 1,
    DeliveryTimeMaxMinutes = 2,
    TaxRate                = 0.045,
    ShippingCost           = 30,
    FreeShippingThreshold  = 475,

    DefaultStock           = 100,
    LowStockPercentage     = 20,
    AllowBackorders        = false,

    ImageBasePath          = "nui://qb-inventory/html/images/",
    Items                  = { --[[ see below ]] }
}
```

### Top-Level Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `DeliveryTimeMinMinutes` | number | Lower bound of random delivery delay after an order is placed (minutes) |
| `DeliveryTimeMaxMinutes` | number | Upper bound of random delivery delay (minutes). Each order picks a random value between min and max |
| `TaxRate` | number | Decimal tax rate applied to each order subtotal. `0.045` = 4.5% |
| `ShippingCost` | number | Flat base shipping fee added to orders |
| `FreeShippingThreshold` | number | Order subtotal at which shipping becomes free |
| `DefaultStock` | number | Starting stock used when an item entry doesn't specify its own `stock` |
| `LowStockPercentage` | number | Threshold (% of `maxStock`) at which a low-stock indicator appears in the management UI |
| `AllowBackorders` | boolean | If `true`, orders can be placed when stock is 0. If `false`, items show as out-of-stock and reject orders |
| `ImageBasePath` | string | NUI base URL for item icons. Auto-set at startup based on detected inventory resource — manually setting this is rarely needed |
| `Items` | table | Catalogue of orderable items (see below) |

## Items Schema

```lua
Items = {
    i4_engine          = { name = "I4 Engine",          category = "engines",      itemKey = "1", price = 18000, stock = 50,  weight = 1000 },
    v6_engine          = { name = "V6 Engine",          category = "engines",      itemKey = "2", price = 28000, stock = 50,  weight = 1000 },
    v8_engine          = { name = "V8 Engine",          category = "engines",      itemKey = "3", price = 42000, stock = 50,  weight = 1000 },
    v12_engine         = { name = "V12 Engine",         category = "engines",      itemKey = "4", price = 58000, stock = 50,  weight = 1000 },
    slick_tyres        = { name = "Slick Tyres",        category = "tyres",        itemKey = "1", price = 12000, stock = 100, weight = 1000 },
    semi_slick_tyres   = { name = "Semi Slick Tyres",   category = "tyres",        itemKey = "2", price = 10000, stock = 100, weight = 1000 },
    offroad_tyres      = { name = "Offroad Tyres",      category = "tyres",        itemKey = "3", price = 9500,  stock = 100, weight = 1000 },
    ceramic_brakes     = { name = "Ceramic Brakes",     category = "brakes",       itemKey = "1", price = 14000, stock = 75,  weight = 1000 },
    awd_drivetrain     = { name = "AWD Drivetrain",     category = "drivetrains",  itemKey = "1", price = 32000, stock = 50,  weight = 1000 },
    rwd_drivetrain     = { name = "RWD Drivetrain",     category = "drivetrains",  itemKey = "2", price = 28000, stock = 50,  weight = 1000 },
    fwd_drivetrain     = { name = "FWD Drivetrain",     category = "drivetrains",  itemKey = "3", price = 25000, stock = 50,  weight = 1000 },
    turbocharger       = { name = "Turbo",              category = "turbocharging",itemKey = "1", price = 22000, stock = 60,  weight = 1000 },
    drift_tuning_kit   = { name = "Drift Tuning Kit",   category = "driftTuning",  itemKey = "1", price = 15000, stock = 50,  weight = 1000 },
    engine_oil         = { name = "Engine Oil",         category = "servicing",                   price = 35,    stock = 5,   weight = 1000 },
    tyre_replacement   = { name = "Tyre Replacement",   category = "servicing",                   price = 1200,  stock = 100, weight = 1000 },
    clutch_replacement = { name = "Clutch Replacement", category = "servicing",                   price = 1800,  stock = 75,  weight = 1000 },
    air_filter         = { name = "Air Filter",         category = "servicing",                   price = 180,   stock = 150, weight = 1000 },
    spark_plug         = { name = "Spark Plug",         category = "servicing",                   price = 55,    stock = 200, weight = 1000 },
    suspension_parts   = { name = "Suspension Parts",   category = "servicing",                   price = 1500,  stock = 75,  weight = 1000 },
    brakepad_replacement = { name = "Brakepad Replacement", category = "servicing",               price = 900,   stock = 100, weight = 1000 },
    nitrous_bottle     = { name = "Nitrous Bottle",     category = "nitrous",                     price = 350,   stock = 150, weight = 1000 },
    nitrous_install_kit= { name = "Nitrous Install Kit",category = "nitrous",                     price = 3500,  stock = 60,  weight = 1000 },
    cosmetic_part      = { name = "Body Kit",           category = "cosmetic",                    price = 3500,  stock = 75,  weight = 1000 },
    vehicle_wheels     = { name = "Vehicle Wheels Set", category = "cosmetic",                    price = 2500,  stock = 100, weight = 1000 },
    respray_kit        = { name = "Respray Kit",        category = "cosmetic",                    price = 1500,  stock = 150, weight = 1000 },
    tyre_smoke_kit     = { name = "Tyre Smoke Kit",     category = "cosmetic",                    price = 800,   stock = 90,  weight = 1000 },
    bulletproof_tyres  = { name = "Bulletproof Tyres",  category = "cosmetic",                    price = 2500,  stock = 60,  weight = 1000 },
    extras_kit         = { name = "Extras Kit",         category = "cosmetic",                    price = 1000,  stock = 80,  weight = 100  },
    performance_part   = { name = "Performance Part",   category = "performance",                 price = 4000,  stock = 75,  weight = 1000 },
    cleaning_kit       = { name = "Cleaning Kit",       category = "repair",                      price = 145,   stock = 200, weight = 1000 },
    repairkit          = { name = "Vehicle Repair Kit", category = "repair",                      price = 525,   stock = 150, weight = 1000 },
    ev_motor           = { name = "EV Motor",           category = "electric",                    price = 89250, stock = 50,  weight = 1000 },
    ev_battery         = { name = "EV Battery",         category = "electric",                    price = 47250, stock = 60,  weight = 1000 },
    ev_coolant         = { name = "EV Coolant",         category = "electric",                    price = 325,   stock = 100, weight = 1000 }
}
```

### Item Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| (item key) | string | Inventory item key. Must match a registered item in your inventory resource |
| `name` | string | Display name shown in the order UI |
| `category` | string | Grouping for the order UI's filter tabs. Valid values: `engines`, `tyres`, `brakes`, `drivetrains`, `turbocharging`, `driftTuning`, `servicing`, `nitrous`, `cosmetic`, `performance`, `repair`, `electric` |
| `itemKey` | string (optional) | Sort key inside the category. `"1"`, `"2"`, `"3"` orders entries within the same category. Omitted on servicing/nitrous/cosmetic/performance/repair/electric where ordering isn't critical |
| `price` | number | Per-unit order price |
| `stock` | number | Starting stock value. Falls back to `Config.Shop.DefaultStock` when omitted |
| `weight` | number | Item weight in grams. Used by inventory systems that track weight (`ox_inventory`, `qs-inventory`, etc.) |

## Stock Behavior

- Each item starts with its `stock` value.
- Restocking happens through the admin tools / order fulfillment flow.
- When stock hits `LowStockPercentage` of its starting value, the UI/management page shows a low-stock indicator.
- When stock = 0 and `AllowBackorders = false`, the item is non-orderable until restocked.

## Image Path

The shop UI loads item icons from your inventory's image folder. The image path is auto-detected at startup based on which inventory resource is running (see [Framework & Integrations](framework-and-integrations.md)). If none of the supported inventories are detected, it falls back to PC-Mechanic's own `public/` folder.

## Walk-Up Parts Shops vs Central Catalogue

| Concept | Where defined | Purpose |
|---------|---------------|---------|
| Central catalogue | `Config.Shop.Items` | Order/delivery/restock prices, stock tracking |
| Walk-up shop | `Config.ShopLocations[shop].shops[].items` | On-counter prices for buy-now mechanics |

A part can appear in both — typically with **different prices**. The walk-up price is what mechanics pay buying parts for an immediate job; the central catalogue price is what they pay when ordering for restock with shipping/tax.

Items on the walk-up shop don't have stock — they're treated as always-available counter items. Stock tracking only applies to the central catalogue.
