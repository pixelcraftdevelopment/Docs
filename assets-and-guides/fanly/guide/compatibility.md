# Phone & Banking Compatibility

## Phone Resources

Fanly registers itself against whichever phone resource is started. No configuration needed — auto-detect handles it.

| Phone | Status | Notes |
|-------|--------|-------|
| **lb-phone** | ✅ Full | Custom app, SMS + native push, mail |
| **yseries** | ✅ Full | Custom app, SMS + mail |
| **gksphone** | ✅ Full | Custom app, native notifications |
| **qs-smartphone** | ✅ Full | Custom app, native notifications |
| **qs-smartphone-pro** | ✅ Full | Custom app, native notifications |
| **qb-phone** | ✅ Full | Custom app, native notifications |
| **17mov_Phone** | ✅ Full | Custom app, separate UI bundle (icon inlined as SVG) |
| **npwd** | ✅ Full | Custom app, native notifications |

If you run more than one phone resource on the same server, Fanly registers against the one started first.

## Frameworks

| Framework | Status |
|-----------|--------|
| **QBCore** | ✅ Full |
| **Qbox** | ✅ Full |
| **ESX** | ✅ Full (legacy and new export styles) |

`Config.Framework = 'auto'` detects automatically. Override only if you have multiple framework resources started simultaneously.

## Banking Resources

Fanly auto-detects an installed banking resource for charges (subs, tips, PPV, paid DMs) and payouts (creator withdraws to bank). Probe order:

1. `pc-banking`
2. `qb-banking`
3. `okokBanking`
4. `Renewed-Banking`
5. `wasabi_banking`
6. `jaksam_billing`
7. `fd_banking`
8. `tgg-banking`
9. `crm-banking`
10. `prism_banking`
11. `p_banking`
12. `justbanks`
13. `RxBanking`
14. `esx_addonaccount`
15. **Framework-native** — `Player.Functions.RemoveMoney` / `AddMoney` (QBCore/Qbox) or `xPlayer.removeAccountMoney` / `addAccountMoney` (ESX). Most modern banking scripts hook these transparently, so this works for many setups even without an explicit integration.
16. **Internal** — Fanly's own `fanly_wallet` table. Fully standalone, useful for testing.

The first started resource wins. To force a specific provider, set `Config.Banking` to its name. See [Banking Integration](../configuration/banking.md).

{% hint style="info" %}
Fanly works with **zero** banking integration. If no banking resource is detected, it falls back to its internal wallet. Players can still subscribe, tip, and unlock — they just can't withdraw to an external bank.
{% endhint %}

## Inventory

Fanly does not interact with inventory in v1 — there are no item-based features.

## Notification Resources

`Config.Notifications = 'auto'` picks the first available of `ox_lib`, `okokNotify`, `ps-ui`, `lation_ui`, `nox_notify`. Used only for in-game toast popups (the phone-side push uses the phone's own notification system).
