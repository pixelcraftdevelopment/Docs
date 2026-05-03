# Configuration

PC-Mechanic config is split across files in `pc-mechanic/config/`:

| File | Contains |
|------|----------|
| `config.lua` | Framework, locale, currency, business toggles, interaction controls, mileage, nitrous, items, stance, minigames, pricing, integrations, roles, repair zones, mechanic jobs, shop locations, Discord webhooks |
| `Inspection.lua` | Serviceable parts, inspection minigames, inspection validity rules |
| `ServicingDamage.lua` | Damage-driven part wear, oil leak system, engine seizure, tyre burst tracking, low-oil shutdowns |
| `Tuning.lua` | Engines, drivetrains, tyres, brakes, drift kits, anti-roll bars, launch control — with handling values and pricing |
| `Shops.lua` | Shop inventory items, prices, stock, delivery times, tax, shipping |
| `modmenu.lua` | Mod menu categories, performance/cosmetics partTypes, plate indexes, window tints, wheel types, horns, paint colours, xenon colours |
| `ElectricVehicles.lua` | EV model whitelist (older builds only — auto-detected on build 3258+) |

## Sub-Pages

### Core

* [Locale, Currency, and Time](locale-and-currency.md)
* [Framework & Integrations](framework-and-integrations.md)
* [Roles & Permissions](roles.md)
* [Mechanic Jobs Whitelist](mechanic-jobs.md)

### Shops & Locations

* [Shop Locations](shops-and-locations.md)
* [Repair Zones](repair-zones.md)
* [Shop Inventory & Pricing](shop-inventory.md)
* [Mod Menu](mod-menu.md)
* [Tuning](tuning.md)

### Vehicle Systems

* [Mileage](mileage.md)
* [Servicing & Inspection](servicing-and-inspection.md)
* [Damage System](damage-system.md)
* [Oil Leak & Engine Seizure](oil-and-seizure.md)
* [Electric Vehicles](electric-vehicles.md)
* [Stance](stance.md)
* [Nitrous](nitrous.md)
* [Dyno](dyno.md)

### Behavior

* [Pricing Engine](pricing.md)
* [Items & Tools](items-and-tools.md)
* [Minigames & Skillchecks](minigames.md)
* [Installation Mode](installation-mode.md)
* [Tablet & Interaction](tablet-and-interaction.md)
* [Commands](commands.md)
* [Discord Webhooks](discord-webhooks.md)
