# Locale, Currency, and Time

Top-level presentation settings in `pc-mechanic/config/config.lua`.

## Locale

```lua
Config.Locale = "en"
```

Available: `en`, `ar`, `cn`, `de`, `es`, `fr`, `hu`, `it`, `ja`, `pt`, `sv`, `zh-tw`.

If a key is missing in the chosen locale, the system falls back to English. If still missing, the raw key name is shown so format strings don't crash silently.

## Currency

```lua
Config.Currency = "USD"
```

Used for currency labels in the UI. Pure display — does not affect framework money handling.

## Time Format

```lua
Config.UseServerTime  = false   -- true = server time, false = local client time
Config.Use24HourFormat = false   -- true = 24h, false = 12h
```

`UseServerTime` controls whether timestamps in the tablet UI (orders, invoices, dyno history) are based on the server's clock or the client's local clock. `Use24HourFormat` is purely formatting.

## Debug

```lua
Config.Debug = false
```

When true, additional debug prints are sent to the console (servicing degradation events, damage classification, oil leak triggers, etc.). Leave off in production — chatty.
