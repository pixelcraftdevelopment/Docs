# Electric Vehicles

Defined in `pc-mechanic/config/ElectricVehicles.lua`.

## The List

```lua
Config.ElectricVehicles = {
    "Airtug",     "buffalo5",   "caddy",
    "Caddy2",     "caddy3",     "coureur",
    "cyclone",    "cyclone2",   "imorgon",
    "inductor",   "iwagen",     "khamelion",
    "metrotrain", "minitank",   "neon",
    "omnisegt",   "powersurge", "raiden",
    "rcbandito",  "surge",      "tezeract",
    "virtue",     "vivanite",   "voltic",
    "voltic2",
}
```

A flat list of model names recognized as electric vehicles.

## Auto-Detection

```
On game build 3258 (Bottom Dollar Bounties) or newer → auto-detected by engine, list ignored
On older builds → list is consulted, models not in the list are treated as combustion
```

The system checks `GetGameBuildNumber()` at runtime. On modern builds, the native `IS_VEHICLE_ELECTRIC` is used and your list is purely a fallback.

## What "Electric" Affects

Whether a vehicle is considered electric flows through:

| System | Combustion | Electric |
|--------|-----------|----------|
| `Config.Servicing` whitelist | engineOil, clutch, airFilter, sparkPlugs apply | evMotor, evBattery, evCoolant apply |
| `Config.Tuning.engines` | All engine swaps available | Engine swaps unavailable (whitelist = combustion) |
| Oil leak system | Active | Skipped |
| Engine seizure at 0% oil | Possible | Skipped |
| Random shutdowns at low part % | Spark plug below threshold | EV battery below threshold |

Other systems (mileage, damage, repair zones, mod menu, stance, dyno, nitrous) apply identically to both vehicle types.

## Adding Custom EVs

If you stream a custom EV model on a pre-3258 build, add its model name to the list:

```lua
Config.ElectricVehicles = {
    "Airtug", "buffalo5", "caddy",
    -- existing entries...
    "myCustomEV",
    "myOtherEV"
}
```

Then restart the resource. Model names are matched case-insensitively against `GetEntityModel`'s string equivalent.

On builds 3258+, custom EVs need their `vehicles.meta` to declare them as electric (the GTA flag is what the native checks). The list isn't consulted.
