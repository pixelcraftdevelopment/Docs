# Framework, Locale, Currency

Top-level runtime and presentation settings in `pc-banking/config/config.lua`.

## Framework

```lua
Config.Framework = 'auto'   -- 'auto' | 'QBCore' | 'Qbox' | 'ESX'
```

- `'auto'` detects framework by started resources at runtime.
- Set explicit value if your server has multiple framework resources present.

## Inventory

```lua
Config.Inventory = 'auto'   -- 'auto' | 'ox_inventory' | 'qb-inventory' | 'qs-inventory' | 'codem-inventory' | 'tgiann-inventory' | 'ak47_inventory' | 'origen_inventory' | 'realrp_inventory' | 'l2s-inventory' | 'esx_inventory'
```

Used for card-item creation and card-item usage checks.

## Notifications and Retention

```lua
Config.Notifications        = 'auto'   -- 'auto' | 'ox_lib' | 'okokNotify' | 'ps-ui' | 'lation_ui' | 'nox_notify'
Config.MaxNotifications     = 50
Config.TransactionCleanupDays = 90
```

- `MaxNotifications` controls in-app list size returned to clients.
- `TransactionCleanupDays` is startup cleanup retention (transactions + notifications older than N days are deleted).

## Locale and Currency

```lua
Config.Locale         = 'en'
Config.CurrencySymbol = '$'
Config.CurrencyLocale = 'en-US'
```

- `Locale` selects locale file key.
- `CurrencyLocale` is the formatting locale used for numeric/currency rendering.

## Debug

```lua
Config.Debug = false
```

Enables additional debug logging paths.

## Brand Logo

```lua
Config.BrandLogoUrl = 'https://cfx-nui-pc-banking/assets/brand.png'
```

Used as the branding image in UI surfaces that consume this config value.
