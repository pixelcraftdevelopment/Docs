# Banking Integration

Controls which banking resource Fanly uses for charging fans (subs, tips, PPV, paid DMs) and paying creators (Studio withdraws).

```lua
Config.Banking = 'auto'
```

## Auto-Detect

`'auto'` walks a priority list at startup and binds to the first started resource:

| Order | Resource | Notes |
|-------|----------|-------|
| 1 | `pc-banking` | PixelCraft Banking |
| 2 | `qb-banking` | QBCore stock |
| 3 | `okokBanking` | OKOK |
| 4 | `Renewed-Banking` | Hooks the framework — uses framework-native paths |
| 5 | `wasabi_banking` | Wasabi explicit exports + framework |
| 6 | `jaksam_billing` | Hooks the framework — uses framework-native paths |
| 7 | `fd_banking` | Hooks the framework — uses framework-native paths |
| 8 | `tgg-banking` | Hooks the framework — uses framework-native paths |
| 9 | `crm-banking` | Hooks the framework — uses framework-native paths |
| 10 | `prism_banking` | Hooks the framework — uses framework-native paths (prism only exposes society + transaction exports) |
| 11 | `p_banking` | Hooks the framework — uses framework-native paths (p_banking exposes society `*AccountMoney` only) |
| 12 | `justbanks` | Hooks the framework — uses framework-native paths (card-based explicit API not used) |
| 13 | `RxBanking` | Hooks the framework — RxBanking personal account is synced with framework bank balance |
| 14 | `esx_addonaccount` | Native ESX bank account |
| 15 | `native` | Framework money APIs only — `Player.Functions.RemoveMoney` / `AddMoney` (QBCore/Qbox) or `xPlayer.removeAccountMoney` / `addAccountMoney` (ESX). Most modern banking scripts hook these transparently |
| 16 | `internal` | Fanly's own `fanly_wallet` table. Fully standalone, test mode |

## Forcing a Provider

Pass the name explicitly to skip auto-detect:

```lua
Config.Banking = 'pc-banking'         -- force pc-banking exports
Config.Banking = 'qb-banking'         -- force qb-banking exports
Config.Banking = 'okokBanking'        -- force okokBanking exports
Config.Banking = 'Renewed-Banking'    -- use framework-native (Renewed hooks them)
Config.Banking = 'wasabi_banking'     -- wasabi explicit + framework
Config.Banking = 'jaksam_billing'     -- framework-native
Config.Banking = 'fd_banking'         -- framework-native
Config.Banking = 'tgg-banking'        -- framework-native
Config.Banking = 'crm-banking'        -- framework-native
Config.Banking = 'prism_banking'      -- framework-native (prism hooks the paths)
Config.Banking = 'p_banking'          -- framework-native (p_banking hooks the paths)
Config.Banking = 'justbanks'          -- framework-native (card-based API not used)
Config.Banking = 'RxBanking'          -- framework-native (synced with bank balance)
Config.Banking = 'esx_addonaccount'   -- framework-native ESX bank account
Config.Banking = 'native'             -- framework money APIs only
Config.Banking = 'internal'           -- fanly_wallet table only
Config.Banking = false                -- same as 'internal'
```

## Internal Wallet

If no banking resource is detected (or you set `'internal'`), Fanly uses its own `fanly_wallet` table:

* Fans need a Fanly wallet balance to spend (no auto-deposit — they have nothing to spend with by default).
* Creators withdraw into the same internal wallet (no real bank).

Use only for testing. For a live server, install any of the supported banking resources or rely on framework-native.

## Cross-Account Safety

When a player is signed in with someone else's credentials, every charge and credit routes to the **real account owner's** bank — never to the player who's typing. This is enforced server-side regardless of which banking provider is active.
