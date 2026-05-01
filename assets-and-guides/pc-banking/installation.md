# Installation

## Prerequisites

* `ox_lib` (required)
* `oxmysql`
* QBCore, Qbox, or ESX framework
* MySQL 5.7+ / MariaDB 10.3+

## Steps

1. **Download** PC-Banking + PC-Banking-Phone from FiveM keymaster
2. **Extract** to `resources/[banking]/pc-banking` and `resources/[banking]/pc-banking-phone`
3. **Database** — run `pc-banking/database/run.sql` against your MySQL database. Creates all required tables. No migrations needed; this is a fresh-install schema.
4. **server.cfg** — add ensure lines AFTER your framework + ox_lib + oxmysql:

```
ensure ox_lib
ensure oxmysql
ensure qb-core   # or es_extended / qbx_core

ensure pc-banking
ensure pc-banking-phone
```

5. **Phone integration** — set `Config.Phone` in `pc-banking/config/config.lua` to match your phone resource (`'auto'` autodetects). Same for `Config.Inventory` and `Config.Notifications`.

{% hint style="warning" %}
PC-Banking REPLACES your framework's stock money handling. Players' existing bank balance is migrated to a primary checking account at `Config.DefaultBank` on first login. Cash is left as-is.
{% endhint %}

## First Run

* Players who already have a framework-side bank balance get a Fleeca primary checking account on first login, balance preserved.
* Brand-new players get an empty primary at the default bank.
* No password is set initially; players configure password on first phone-app or desktop UI open.

## Optional: Backwards-Compatibility

If your server has legacy resources expecting `qb-banking`, `qb-management`, `Renewed-Banking`, `esx_addonaccount`, or `okokBanking` exports, enable shims:

```lua
-- pc-banking/config/config.lua
Config.Compat = {
    qb_banking      = true,
    qb_management   = true,
    renewed_banking = true,
    esx_addonaccount = true,
    okok_banking    = true,
}
```

See [Backwards Compatibility](backwards-compat.md) for the export surface each shim exposes.
