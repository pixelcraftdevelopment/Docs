# Nitrous

```lua
Config.BoostKey               = "RMENU"
Config.BoostMultiplier        = 2.0
Config.BoostTime              = 10
Config.BoostCooldown          = 5
Config.BoostMaxBottle         = 3
Config.BoostPurgingDrainRate  = 0.1
Config.BoostAllowPartialRefill = true
```

| Field | Purpose |
|-------|---------|
| `BoostKey` | Activation control. Default `RMENU` (right-click menu key). Accepts any FiveM control name |
| `BoostMultiplier` | Speed multiplier while boosting. 2.0 = double current speed |
| `BoostTime` | Boost duration in seconds per activation |
| `BoostCooldown` | Mandatory wait between activations in seconds |
| `BoostMaxBottle` | Maximum bottles a single vehicle can hold |
| `BoostPurgingDrainRate` | How fast purging drains the system per cycle |
| `BoostAllowPartialRefill` | If true, a half-empty system can accept a single bottle to top up |

## Items

Two items drive the nitrous economy:

| Item | Role |
|------|------|
| `nitrous_install_kit` | One-time install per vehicle (3500 default price) |
| `nitrous_bottle` | Single bottle of charge (350 default price) |

The install kit is required once. After install, each bottle item adds one charge slot up to `BoostMaxBottle`.

## Refill Behavior

With `BoostAllowPartialRefill = true`:
- A car with 2 empty bottle slots and 1 full can have one bottle added to fill an empty slot
- Players can refill bottle-by-bottle as they earn money

With `BoostAllowPartialRefill = false`:
- The system must be fully drained before a refill is accepted
- Cleaner economy but more punishing

## Permission

Nitrous installation is gated by:

- `Config.ShopLocations[shop].mods.performance.enabled` — performance category enabled at the shop
- Per-role `canInstallNitrous` permission
- The `nitrous_install_kit` (or bottle) item in inventory

By default every shop role has `canInstallNitrous = true`. Set it to false on lower roles if you want to gate this to senior staff only.

## Purging

Purging is a visible jet of nitrous from the system. It's purely cosmetic but uses real charge — `BoostPurgingDrainRate` per cycle of purging. Players who purge for show have less actual boost left.
