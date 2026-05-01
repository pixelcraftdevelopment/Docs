# Compatibility

## Frameworks & Phones

- QBCore, Qbox, ESX - auto-detected.
- lb-phone, yseries, qs-smartphone, qs-smartphone-pro, qb-phone, gksphone, 17mov_Phone, npwd - auto-detected.
- ox_inventory, qb-inventory, qs-inventory, codem, tgiann, ak47, origen, realrp, l2s, esx_inventory - supported.
- Notification scripts: ox_lib, okokNotify, ps-ui, lation_ui, nox_notify.

## Drop-In Replacement Shims

PC Banking exposes the same exports and events as common legacy banking and management resources, so existing scripts that depend on them keep working without changes:

- qb-banking, qb-management
- Renewed-Banking
- esx_addonaccount, esx_society
- okokBanking (and v2)
- qs-banking, tgg-banking, rx-banking, omes_banking, fd_banking

Each shim has three modes: **auto** (only bind if the real resource is not started - default and safe), **force** (always bind, useful when migrating), or **off**. Toggle them in the compat config.

## Economy Tuning

All scheduled timings - interest accrual, monthly fees, EMI cadence, credit billing cycle, annual card fees - live in a single block of the main config. The defaults assume **7 real days = 1 in-game month** and **84 real days = 1 in-game year**, but you can speed up or slow down the whole economy by editing those numbers.

