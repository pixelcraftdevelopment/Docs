# Locations and ATMs

Defined in `pc-banking/config/locations.lua`. This file controls world interaction points, bank branch service menus, ATM behavior, and inter-bank ATM fees.

## Top-Level Flags

```lua
Config.UseTarget = true
Config.ShowBlips = true
Config.SpawnBankPeds = true
Config.EnableATMs = true
```

| Field | Type | Notes |
|-------|------|-------|
| `UseTarget` | bool | Uses `ox_target`/`qb-target` zones if available; falls back to proximity mode when unavailable |
| `ShowBlips` | bool | Creates map blips for each `BankLocations` entry |
| `SpawnBankPeds` | bool | Spawns configured teller peds at branch locations |
| `EnableATMs` | bool | Enables ATM model interaction + ATM DUI flow |

## `Config.BankLocations`

```lua
Config.BankLocations = {
  {
    coords   = vector3(...),
    heading  = 340.0,
    label    = 'Fleeca Downtown',
    bank     = 'fleeca',
    services = { 'deposit', 'withdraw', 'transfer', 'cards', 'savings', 'loans' },
    blip     = { sprite = 108, color = 2, scale = 0.8 },
    spawnPed = true,
    ped      = { model = 'u_m_m_bankman', scenario = 'WORLD_HUMAN_CLIPBOARD' },
  }
}
```

| Field | Type | Notes |
|-------|------|-------|
| `coords` | vector3 | Interaction and blip world position |
| `heading` | number | Facing direction for ped/zone |
| `label` | string | Branch label shown in UI and on map |
| `bank` | string | Bank key from `Config.Banks` |
| `services` | table | Enabled features at this branch (UI menu gating) |
| `blip.sprite` | number | Blip sprite id |
| `blip.color` | number | Blip color id |
| `blip.scale` | number | Blip scale |
| `spawnPed` | bool | Per-location ped override (`false` disables at this branch) |
| `ped.model` | string | Ped model name |
| `ped.scenario` | string | Idle scenario task |

## `Config.ATMModels`

```lua
Config.ATMModels = {
  ['prop_fleeca_atm'] = { banks = { 'fleeca' } },
  ['prop_atm_03']     = { banks = { 'fleeca', 'maze', 'pacific' } },
}
```

| Field | Type | Notes |
|-------|------|-------|
| model key | string | World prop model name |
| `banks` | table | Allowed bank ids for that ATM model |

Behavior:
1. One-bank model -> always that bank.
2. Multi-bank model -> resolves to nearest configured branch among allowed banks.
3. Missing/empty mapping -> falls back to `Config.DefaultBank`.

## ATM Access and Security

```lua
Config.ATMServices = { 'deposit', 'withdraw' }
Config.ATMRequiresCard = false
Config.ATMAllowOtherCards = true
Config.ATMAllowCreditCards = true
Config.ATMWrongPinAlertAfter = 3
```

| Field | Type | Notes |
|-------|------|-------|
| `ATMServices` | table | Services exposed in ATM context |
| `ATMRequiresCard` | bool | If `true`, player must carry at least one configured card item to open ATM |
| `ATMAllowOtherCards` | bool | Allows using cards found in inventory even if card owner differs |
| `ATMAllowCreditCards` | bool | Allows credit-card cash advances at ATM |
| `ATMWrongPinAlertAfter` | number | Wrong-PIN alert threshold to card owner (`0` disables alerts) |

Note: ATM wrong-PIN lockout escalates further and auto-locks card after higher repeated failures.

## `Config.InterBankFees`

```lua
Config.InterBankFees = {
  enabled = true,
  defaultFee = 100,
  fees = {
    ['fleeca'] = { ['maze'] = 100, ['pacific'] = 125 },
  },
  noFeePartners = {
    -- { 'fleeca', 'maze' },
  },
}
```

| Field | Type | Notes |
|-------|------|-------|
| `enabled` | bool | Master switch for inter-bank ATM fees |
| `defaultFee` | number | Fallback fee when no explicit pair override matches |
| `fees` | table | Nested matrix: `fees[atmBank][cardBank] = fee` |
| `noFeePartners` | table | Bidirectional bank-pair exemptions |

Fee evaluation order: disabled -> same bank -> no-fee partner -> per-pair override -> `defaultFee`.
