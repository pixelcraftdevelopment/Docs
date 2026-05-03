# Items & Tools

Block of related settings in `pc-mechanic/config/config.lua` that govern the player-usable items the system ships with.

## Repair Kit

```lua
Config.RepairKitItem        = "repairkit"
Config.RepairKitMechanicOnly = true
Config.RepairKitRemoveOnUse  = true
```

| Field | Purpose |
|-------|---------|
| `RepairKitItem` | Inventory item name to use for vehicle repair |
| `RepairKitMechanicOnly` | If true, only mechanics (job in `Config.MechanicJobs`) can use the kit |
| `RepairKitRemoveOnUse` | If true, the item is consumed on use |

The repair kit name is also referenced from `Config.Mods.ItemsRequired.repair.itemName` — they stay in sync if you change `RepairKitItem`.

A repair kit restores body and engine health to 100%. It does **not** restore servicing parts (oil, tyres, etc.) — those need their own replacement items.

## Oil Leak Repair

```lua
Config.OilLeakRepairItem        = "blowtorch"
Config.OilLeakRepairItemRemove  = false
Config.OilLeakRepairMechanicOnly = true
```

| Field | Purpose |
|-------|---------|
| `OilLeakRepairItem` | Item used to seal an oil leak |
| `OilLeakRepairItemRemove` | If true, item is consumed on use |
| `OilLeakRepairMechanicOnly` | If true, only mechanics can repair leaks |

Default `blowtorch` is reusable — sealing a leak doesn't consume it. Set `OilLeakRepairItemRemove = true` for a consumable economy.

## Engine Replacement

```lua
Config.EngineReplacementItem        = "engine_replacement"
Config.EngineReplacementMechanicOnly = true
Config.EngineReplacementRemoveOnUse  = true
```

The high-end recovery item for seized engines. Cross-references `Config.Tuning.engines[5]` (the engine replacement entry, `requiresSeizedEngine = true`).

## Turbocharger

```lua
Config.TurbochargerItem         = "turbocharger"
Config.TurbochargerMechanicOnly = true
Config.TurbochargerRemoveOnUse  = true
```

The turbocharger item drives the toggle on `Config.Mods.Performance` for `partType = 18` (`Turbocharging`, `toggle = true`).

## Mechanic-Only Items Pattern

All four of these tools share a `MechanicOnly` and `RemoveOnUse` flag pattern. The conventions:

- `MechanicOnly = true` (default) — restricts use to players whose framework job is in `Config.MechanicJobs`. Customers can still buy the items, but only mechanics can use them.
- `RemoveOnUse = true` (default for kits/replacements) — consumes the item on use.

If you want a customer-self-service flow (e.g. "any player can use a repair kit anywhere"), set `RepairKitMechanicOnly = false`. That decouples the kit from the mechanic gate but doesn't bypass repair zones — those still apply to mechanics, but a non-mechanic using a kit out in the world isn't bound by them.

## Item Names in Multiple Places

Some items appear in multiple config blocks. Keep them consistent:

| Item | Config keys it appears in |
|------|---------------------------|
| `repairkit` | `Config.RepairKitItem`, `Config.Mods.ItemsRequired.repair.itemName`, `Config.Shop.Items.repairkit`, walk-up shop items |
| `engine_replacement` | `Config.EngineReplacementItem`, `Config.Tuning.engines[5].itemName` |
| `nitrous_install_kit` | `Config.Shop.Items`, walk-up shop items |
| `blowtorch` | `Config.OilLeakRepairItem` (typically also exists in your inventory's items table) |

Renaming any item means updating all the references. For some, it propagates automatically (e.g. `Config.Mods.ItemsRequired.repair.itemName = Config.RepairKitItem or "repairkit"`); for others you need to update by hand.

## Inventory Registration

Items must exist in your inventory resource (`ox_inventory`'s items.lua, qb-core's items list, etc.). PC-Mechanic does not register items into the inventory — you need to add them yourself. The `pc-mechanic/inventory/` folder ships ready-to-paste configurations for popular inventory resources.
