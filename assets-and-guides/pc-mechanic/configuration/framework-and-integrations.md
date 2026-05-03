# Framework & Integrations

All integrations default to `"auto"` and detect at runtime by checking which resources are started. Override only if you have multiple competing resources.

## Framework

```lua
Config.Framework = "auto"   -- "auto", "QBCore", "Qbox", "ESX"
```

## Inventory

```lua
Config.Inventory = "auto"
-- "auto", "ox_inventory", "qb-inventory", "qs-inventory", "codem-inventory",
-- "tgiann-inventory", "ak47_inventory", "origen_inventory", "realrp_inventory",
-- "jaksam_inventory", "esx_inventory", "l2s-inventory"
```

Used for item creation, item-usage callbacks, stash registration, and the shop UI's image base path.

The shop image base path auto-rewires based on detected inventory:

| Inventory | Image base |
|-----------|-----------|
| ox_inventory | `nui://ox_inventory/web/images/` |
| ps-inventory | `nui://ps-inventory/html/images/` |
| qs-inventory | `nui://qs-inventory/html/images/` |
| codem-inventory | `nui://codem-inventory/html/images/` |
| tgiann-inventory | `nui://tgiann-inventory/html/images/` |
| origen_inventory | `nui://origen_inventory/html/images/` |
| qb-inventory | `nui://qb-inventory/html/images/` |
| (none detected) | `nui://pc-mechanic/public/` |

## Notifications

```lua
Config.Notifications = "auto"
-- "auto", "ox_lib", "okokNotify", "ps-ui", "nox_notify", "lation_ui"
```

## Progress Bar

```lua
Config.ProgressBar = "ox-bar"   -- "ox-circle", "ox-bar", "lation_ui", "qb"
```

Used during installation, inspection, and servicing minigames.

## Skill Check

```lua
Config.SkillCheck = "auto"   -- "auto", "ox", "qb", "lation_ui"
```

Drives the skillbar timing minigames (when `Config.UseSkillbars = true`).

## Draw Text

```lua
Config.DrawText = "auto"
-- "auto", "ox_lib", "okokTextUI", "ps-ui", "ZSX_UIV2", "lation_ui", "qb-core"
```

Used for prompts when standing near interaction zones.

## Menus

```lua
Config.Menus = "ox"   -- "ox", "lation_ui"
```

Used for any list/option menus.

## Target System

```lua
Config.Target = "auto"   -- "auto", "ox_target", "qb-target"
```

Drives target prompts on shop ped-models, vehicles for inspection, dyno platforms, parts shop counters.

## Society Banking

```lua
Config.SocietyBanking = "auto"
-- "auto", "qb-banking", "qb-management", "Renewed-Banking", "esx_addonaccount",
-- "okokBanking", "fd_banking", "wasabi_banking", "RxBanking", "justbanks",
-- "tgg-banking", "crm-banking", "prism_banking", "p_banking"
```

Selects the external banking resource for society fund storage. Only used when `Config.UseExternalBanking = true`. Otherwise society funds live inside `pc-mechanic`'s own database.

## Internal vs External Banking

```lua
Config.UseExternalBanking = false   -- false = use built-in society funds, true = use external
Config.SocietyMoneyAccess = true    -- allow paying with society funds at all
Config.PlayerBalance      = "bank"  -- default account type for player payments ("bank", "cash", etc.)
```

Three settings work together:

- `UseExternalBanking` decides **where** society funds live.
- `SocietyMoneyAccess` decides **whether** society pay is allowed at all (per-shop and per-role flags layer on top).
- `PlayerBalance` is the **fallback account** when a player pays for service — typically their main bank account.

## Internal Job System

```lua
Config.InternalFrameworkJobsystem = true
```

- `true` — pulls employee lists from your framework's job system (recommended).
- `false` — uses an internal database table instead. Useful if you want shop staff to be independent of framework jobs.
