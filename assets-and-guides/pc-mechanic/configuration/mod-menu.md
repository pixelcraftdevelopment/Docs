# Mod Menu

`pc-mechanic/config/modmenu.lua` defines what shows up inside each mod category in the customization UI. This is decorative metadata + GTA part-type bindings — not new mechanics, but the catalogue.

## Items Required (Master Map)

```lua
Config.Mods.ItemsRequired = {
    repair           = { itemName = "repairkit",        removeItem = true },
    performance      = { itemName = "performance_part", removeItem = true },
    cosmetics        = { itemName = "cosmetic_part",    removeItem = true },
    stance           = { itemName = "stancing_kit",     removeItem = false },
    respray          = { itemName = "respray_kit",      removeItem = true },
    wheels           = { itemName = "vehicle_wheels",   removeItem = true },
    neonLights       = { itemName = "lighting_kit",     removeItem = true },
    headlights       = { itemName = "lighting_kit",     removeItem = true },
    tyreSmoke        = { itemName = "tyre_smoke_kit",   removeItem = true },
    bulletproofTyres = { itemName = "bulletproof_tyres", removeItem = true },
    extras           = { itemName = "extras_kit",       removeItem = true }
}
```

| Field | Purpose |
|-------|---------|
| `itemName` | Item required in inventory to perform this mod category |
| `removeItem` | Whether the item is consumed (`true`) or kept after use (`false`) |

The repair entry's `itemName` reads from `Config.RepairKitItem` if set (so changing the global repair item name flows through automatically).

## Performance Mods

```lua
Config.Mods.Performance = {
    { partType = 11, name = "Engine",        overrideOptions = {
        { partNum = 0, name = "EMS Upgrade, Level 1" },
        { partNum = 1, name = "EMS Upgrade, Level 2" },
        { partNum = 2, name = "EMS Upgrade, Level 3" },
        { partNum = 3, name = "EMS Upgrade, Level 4" }
    } },
    { partType = 12, name = "Brakes",        overrideOptions = {
        { partNum = 0, name = "Street Brakes" },
        { partNum = 1, name = "Sport Brakes" },
        { partNum = 2, name = "Race Brakes" }
    } },
    { partType = 13, name = "Transmission",  overrideOptions = {
        { partNum = 0, name = "Street Transmission" },
        { partNum = 1, name = "Sports Transmission" },
        { partNum = 2, name = "Race Transmission" }
    } },
    { partType = 15, name = "Suspension",    overrideOptions = {
        { partNum = -1, name = "Stock Suspension" },
        { partNum = 0,  name = "Lowered Suspension" },
        { partNum = 1,  name = "Street Suspension" },
        { partNum = 2,  name = "Sport Suspension" },
        { partNum = 3,  name = "Competition Suspension" }
    } },
    { partType = 16, name = "Armour",        overrideOptions = {
        { partNum = 0, name = "Armor Upgrade 20%" },
        { partNum = 1, name = "Armor Upgrade 40%" },
        { partNum = 2, name = "Armor Upgrade 60%" },
        { partNum = 3, name = "Armor Upgrade 80%" },
        { partNum = 4, name = "Armor Upgrade 100%" }
    } },
    { partType = 18, name = "Turbocharging", toggle = true }
}
```

### Performance Entry Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `partType` | number | GTA `MOD_TYPE` ID. `11` = engine EMS, `12` = brakes, `13` = transmission, `15` = suspension, `16` = armour, `18` = turbo |
| `name` | string | Category display name in the performance menu |
| `overrideOptions` | table (optional) | Array of `{ partNum, name }` rows replacing GTA's default level labels with custom text |
| `toggle` | boolean (optional) | If true, the entry is a single on/off switch instead of a leveled list. Used by Turbocharging |

### `overrideOptions[]` Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `partNum` | number | GTA mod level index. `-1` = stock, `0`+ = upgrade levels |
| `name` | string | Display name shown in the option list |

### Turbocharging Special Case

Turbocharging uses `toggle = true` because GTA exposes it as a binary flag (`SET_VEHICLE_MOD` with `partType = 18`). The toggle requires the `turbocharger` item from `Config.TurbochargerItem`, consumed if `Config.TurbochargerRemoveOnUse = true`.

## Cosmetic Mods

```lua
Config.Mods.Cosmetics = {
    { partType = 0,  name = "Spoilers" },
    { partType = 1,  name = "Front Bumper" },
    { partType = 2,  name = "Rear Bumper" },
    { partType = 3,  name = "Side Skirt" },
    { partType = 4,  name = "Exhaust" },
    { partType = 5,  name = "Chassis" },
    { partType = 6,  name = "Grill" },
    { partType = 7,  name = "Bonnet" },
    { partType = 8,  name = "Left Wing" },
    { partType = 9,  name = "Right Wing" },
    { partType = 10, name = "Roof" },
    { partType = 14, name = "Horn",            ignorePriceMult = true },
    { partType = 19, name = "Subwoofer" },
    { partType = 21, name = "Hydraulics" },
    { partType = 25, name = "Plate Holders" },
    { partType = 26, name = "Vanity Plate" },
    { partType = 27, name = "Trim Design" },
    { partType = 28, name = "Ornaments" },
    { partType = 29, name = "Dashboard" },
    { partType = 30, name = "Dial Design" },
    { partType = 31, name = "Door Speaker" },
    { partType = 32, name = "Seats" },
    { partType = 33, name = "Steering Wheel" },
    { partType = 34, name = "Shift Lever" },
    { partType = 35, name = "Plaques" },
    { partType = 36, name = "ICE" },
    { partType = 37, name = "Trunk" },
    { partType = 38, name = "Hydraulics" },
    { partType = 39, name = "Engine Block" },
    { partType = 40, name = "Air Filter/Boost" },
    { partType = 41, name = "Struts" },
    { partType = 42, name = "Arch Cover" },
    { partType = 43, name = "Aerials" },
    { partType = 44, name = "Trim" },
    { partType = 45, name = "Tank" },
    { partType = 46, name = "Door Left" },
    { partType = 47, name = "Door Right" },
    { partType = 48, name = "Stickers" },
    { partType = 49, name = "Lightbar" },

    { partType = "LIVERY",        name = "Livery" },
    { partType = "LIVERY_ROOF",   name = "Livery Roof" },
    { partType = "PLATE_INDEX",   name = "Plate Index",  ignorePriceMult = true },
    { partType = "WINDOW_TINT",   name = "Window Tint",  ignorePriceMult = true }
}
```

### Cosmetic Entry Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `partType` | number \| string | GTA `MOD_TYPE` ID for numeric entries, or one of the four named keys (`"LIVERY"`, `"LIVERY_ROOF"`, `"PLATE_INDEX"`, `"WINDOW_TINT"`) for special handling |
| `name` | string | Category display name |
| `ignorePriceMult` | boolean (optional) | If true, this cosmetic ignores the per-shop `multiplier` and `vehiclevaluePortion`. Final price is the flat base. Useful for cheap touches (horn, plate index, window tint) that shouldn't scale with vehicle value |

### Named-Key Behaviour

| Key | Backed by |
|-----|-----------|
| `LIVERY` | Vehicle livery slot — uses native `SET_VEHICLE_LIVERY` |
| `LIVERY_ROOF` | Roof livery — uses native `SET_VEHICLE_ROOF_LIVERY_MOD` |
| `PLATE_INDEX` | Plate background — options come from `Config.Mods.PlateIndexes` |
| `WINDOW_TINT` | Window tint — options come from `Config.Mods.WindowTints` |

## Plate Indexes, Window Tints, Wheel Types, Horns

Each is a flat array of entries. Common shape: `{ partNum, name }` plus optional flags.

### `Config.Mods.PlateIndexes`

```lua
{ partNum = 0,  name = "Blue On White" }
{ partNum = 1,  name = "Yellow On Black" }
{ partNum = 2,  name = "Yellow On Blue" }
{ partNum = 3,  name = "Blue On White" }
{ partNum = 4,  name = "Blue On White" }
{ partNum = 5,  name = "North Yankton" }
-- Chop Shop DLC (mp2023_02) only:
{ partNum = 6,  name = "eCola" }
{ partNum = 7,  name = "Las Venturas" }
{ partNum = 8,  name = "Liberty City" }
{ partNum = 9,  name = "Los Santos Car Meet" }
{ partNum = 10, name = "Los Santos Panic" }
{ partNum = 11, name = "Los Santos Pounders" }
{ partNum = 12, name = "Sprunk" }
```

| Field | Type | Purpose |
|-------|------|---------|
| `partNum` | number | GTA plate index value passed to `SET_VEHICLE_NUMBER_PLATE_TEXT_INDEX` |
| `name` | string | Display name |

Removing entries from this list hides them from the plate selector. Plate indexes 6–12 won't show or apply unless the server is on a build with the Chop Shop DLC streamed.

### `Config.Mods.WindowTints`

```lua
{ partNum = 0, name = "No Tint" }
{ partNum = 3, name = "Lightsmoke" }
{ partNum = 2, name = "Darksmoke" }
{ partNum = 1, name = "Pure Black" }
```

The `partNum` order is intentional — GTA's tint indices don't map cleanly to "lightest → darkest", so the list is hand-ordered for a sensible UI sequence.

### `Config.Mods.WheelTypes`

```lua
{ partNum = 0,  name = "Sport" }
{ partNum = 1,  name = "Muscle" }
{ partNum = 2,  name = "Lowrider" }
{ partNum = 3,  name = "SUV" }
{ partNum = 4,  name = "Offroad" }
{ partNum = 5,  name = "Tuner" }
{ partNum = 6,  name = "Bike" }
{ partNum = 7,  name = "High End" }
{ partNum = 8,  name = "Benny's Original" }
{ partNum = 9,  name = "Benny's Bespoke" }
{ partNum = 10, name = "Open Wheel" }
{ partNum = 11, name = "Street" }
{ partNum = 12, name = "Track" }
```

`partNum` is the wheel-type index. The actual wheel models inside each type come from GTA — pick a type, then pick a specific wheel inside that type via the wheels mod menu.

### `Config.Mods.Horns`

```lua
{ partNum = -1, name = "Stock",       musical = false }
{ partNum = 0,  name = "Truck Horn",  musical = false }
{ partNum = 1,  name = "Cop Horn",    musical = false }
-- ...
{ partNum = 3,  name = "Musical Horn 1", musical = true }
-- ...
{ partNum = 57, name = "Air Horn High",  musical = false }
```

| Field | Type | Purpose |
|-------|------|---------|
| `partNum` | number | GTA horn ID (`-1` = stock) |
| `name` | string | Display name |
| `musical` | boolean | If true, the horn plays a musical tune. Used by the UI to group musical horns separately and (depending on shop config) gate them behind a different price tier or category |

58 entries by default, covering classical, jazz, festive, anthem, and air-horn variants.

## Paint Colours

```lua
Config.Mods.Colours = {
    { name = "Primary",     paintTypeKey = "paintType1", colourKey = "color1" },
    { name = "Secondary",   paintTypeKey = "paintType2", colourKey = "color2" },
    { name = "Pearlescent", colourIdKey = "pearlescentColor" },
    { name = "Dashboard",   colourIdKey = "dashboardColor" },
    { name = "Interior",    colourIdKey = "interiorColor" },
    { name = "Wheels",      colourIdKey = "wheelColor" }
}

Config.Mods.RgbPaintFinishes = {
    "Normal", "Metallic", "Pearl", "Matte", "Metal", "Chrome", "Chameleon"
}
```

### `Config.Mods.Colours` Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `name` | string | Display label for the slot in the paint UI |
| `paintTypeKey` | string (optional) | Key on the saved colour table that stores the **finish** (Normal/Metallic/Pearl/Matte/Metal/Chrome/Chameleon). Present only on Primary and Secondary, since only those slots have a finish concept in GTA |
| `colourKey` | string (optional) | Key that stores the colour ID alongside the finish. Present on Primary and Secondary |
| `colourIdKey` | string (optional) | Key that stores a single colour ID (no finish). Present on Pearlescent, Dashboard, Interior, Wheels — slots that are flat colour assignments without a finish |

Primary/Secondary use the `paintTypeKey` + `colourKey` pair because finish and colour are independent for those slots. The other four use a single `colourIdKey` because they're plain colour assignments.

### `Config.Mods.RgbPaintFinishes`

A flat array of finish names. The **index** maps to GTA's paint type ID:

| Index | Finish |
|-------|--------|
| 1 | Normal |
| 2 | Metallic |
| 3 | Pearl |
| 4 | Matte |
| 5 | Metal |
| 6 | Chrome |
| 7 | Chameleon |

{% hint style="warning" %}
The order of `RgbPaintFinishes` is **load-bearing** — it maps to GTA paint type indices. You can rename items but not reorder them.
{% endhint %}

## Colour Tables

```lua
Config.Mods.GtaColours = {
    Metallic  = { { partNum = 0,   name = "Black",          hex = "0d1116" }, --[[ ... ]] },
    Matte     = { { partNum = 12,  name = "Black",          hex = "13181f" }, --[[ ... ]] },
    Util      = { { partNum = 15,  name = "Black",          hex = "151921" }, --[[ ... ]] },
    Worn      = { { partNum = 21,  name = "Black",          hex = "1e232f" }, --[[ ... ]] },
    Misc      = { { partNum = 117, name = "Brushed Steel",  hex = "6a747c" }, --[[ ... ]] },
    Chameleon = { { partNum = 161, name = "Anodized Red",   hex = "CF1020" }, --[[ ... ]] }
}
```

### `Config.Mods.GtaColours` Bucket Counts

| Bucket | Default entry count | partNum range |
|--------|---------------------|---------------|
| `Metallic` | ~95 | 0–11, 27–38, 49–54, 61–74, 88–112, 125, 137, 141–146, 150 |
| `Matte` | 21 | 12–14, 39–42, 55, 82–84, 128–131, 148–149, 151–155 |
| `Util` | 22 | 15–20, 43–45, 56–57, 75–81, 108–110, 122 |
| `Worn` | 28 | 21–26, 46–48, 58–60, 85–87, 113–116, 121, 123–124, 126, 130, 132–133 |
| `Misc` | 16 | 117–120, 127, 134–136, 138–140, 144, 147, 156–159 |
| `Chameleon` | ~82 | 161–242 |

### Per-Colour Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `partNum` | number | GTA colour ID passed to `SET_VEHICLE_COLOURS` / `SET_VEHICLE_EXTRA_COLOURS` / `SET_VEHICLE_INTERIOR_COLOR` etc. |
| `name` | string | Display name shown under the swatch |
| `hex` | string | Hex code for the UI swatch (no `#` prefix). Approximates the in-game colour for quick visual picking |

The bundled `data/carcols_gen9.meta` and `data/carmodcols_gen9.meta` (auto-streamed via `fxmanifest.lua`) wire up extended chameleon and prismatic colours that the stock game doesn't ship with — this is why entries go up to `partNum 242`. If your server streams a competing `carcols.meta`, load order decides which wins.

## Xenon Colours

```lua
Config.Mods.XenonColours = {
    { partNum = 0,  name = "White",          hex = "DEDEFF" },
    { partNum = 1,  name = "Blue",           hex = "0215FF" },
    { partNum = 2,  name = "Electric Blue",  hex = "0353FF" },
    { partNum = 3,  name = "Mint Green",     hex = "00FF8C" },
    { partNum = 4,  name = "Lime Green",     hex = "5EFF01" },
    { partNum = 5,  name = "Yellow",         hex = "FFFF00" },
    { partNum = 6,  name = "Golden Shower",  hex = "FF9600" },
    { partNum = 7,  name = "Orange",         hex = "FF3E00" },
    { partNum = 8,  name = "Red",            hex = "FF0101" },
    { partNum = 9,  name = "Pony Pink",      hex = "FF3264" },
    { partNum = 10, name = "Hot Pink",       hex = "FF05BE" },
    { partNum = 11, name = "Purple",         hex = "2301FF" },
    { partNum = 12, name = "Blacklight",     hex = "0F03FF" }
}
```

### Xenon Sub-Fields

| Field | Type | Purpose |
|-------|------|---------|
| `partNum` | number | GTA xenon colour ID passed to `SET_VEHICLE_HEADLIGHT_COLOR` |
| `name` | string | Display name |
| `hex` | string | Hex swatch for the UI |

13 xenon options. Headlights mod requires the `lighting_kit` item (shared with neon lights via `Config.Mods.ItemsRequired`).

## Adding Custom Cosmetics

1. Find the GTA `MOD_TYPE` you want to expose — see [GTA modkit references](https://docs.fivem.net/natives/?_0xC1F981A6F74F0C23) for the list.
2. Add a row to `Config.Mods.Cosmetics`:
   ```lua
   { partType = 50, name = "My Custom Mod" }
   ```
3. Restart the resource.

If your cosmetic should be free of the price-by-value multiplier, add `ignorePriceMult = true`.
