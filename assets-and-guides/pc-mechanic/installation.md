# Installation

## Prerequisites

* `ox_lib` (required)
* `oxmysql` (required — used by mileage, dyno history, and shop persistence)
* `pc-mechanic-props` (required — bundles dyno platform, inspection tool props)
* QBCore, Qbox, or ESX framework
* MySQL 5.7+ / MariaDB 10.3+
* OneSync enabled

## Steps

1. **Download** `pc-mechanic` from FiveM keymaster.
2. **Extract** to `resources/[mechanic]/pc-mechanic` and place `pc-mechanic-props` alongside.
3. **Database** — run `pc-mechanic/database/run.sql` against your MySQL database.
4. **server.cfg** — add ensure lines AFTER your framework + ox\_lib + oxmysql:

```
setr sv_stateBagStrictMode false --Disable Strict Mode Statebags blocking

ensure ox_lib
ensure oxmysql
ensure qb-core   # or es_extended / qbx_core

ensure pc-mechanic-props
ensure pc-mechanic
```

5. **Stream files** — the resource auto-streams `data/carcols_gen9.meta`, `data/carmodcols_gen9.meta`, and the audio bank (`audiodirectory/pc-mechanic.awc` + `data/pc-mechanic_sounds.dat54.rel`). No manual streaming setup needed.
6. **Auto-detection** — `Config.Framework`, `Config.Inventory`, `Config.Notifications`, `Config.Target`, `Config.SkillCheck`, `Config.DrawText`, and `Config.SocietyBanking` default to `"auto"` and detect at runtime. Override only if you run multiple competing resources.

{% hint style="warning" %}
PC-Mechanic ships with custom `carcols_gen9.meta` and `carmodcols_gen9.meta` files that add chameleon paints, prismatic finishes, and matching xenon colours. If you also stream a different `carcols.meta`, the last loaded one wins — load order matters.
{% endhint %}

## Optional Add-ons

### External Minigames

To use the polished inspection minigames (OBD, pressure, multimeter, tread):

```
ensure pc-mechanic-minigames
```

Then in `pc-mechanic/config/config.lua`:

```lua
Config.UseExternalMinigames = true
```

Each individual minigame can also opt in or out via the per-minigame `useExternal` field (`"default"`, `"yes"`, `"no"`).

### Phone / Tablet UI Notifications

If your server uses one of the auto-detected notification systems (`ox_lib`, `okokNotify`, `ps-ui`, `lation_ui`, `nox_notify`), no further setup is needed.

## First Run

* Self-service shops (Benny's, LSPD garage) work out of the box for any player.
* Owned shops (LS Customs) require at least one player with the framework job set in `Config.MechanicJobs` to access the tablet and management.
* Mileage tracking starts the moment a player drives an owned vehicle. Non-owned vehicles are auto-purged unless `Config.AutoPurgeNonOwnedVehicles = false`.
* Banking integration auto-detects on first transaction. Set `Config.UseExternalBanking = true` if you want society funds to live in your existing banking resource.
