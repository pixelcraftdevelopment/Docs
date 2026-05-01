# pc-banking-phone Config

Phone companion configuration in `pc-banking-phone/config.lua`. Most fields mirror pc-banking — tune here without touching pc-banking.

## Framework Detection

```lua
Config.Framework     = 'auto'   -- 'auto' | 'QBCore' | 'Qbox' | 'ESX'
Config.Phone         = 'auto'   -- 'auto' | 'lb-phone' | 'qs-smartphone' | 'qb-phone' | 'npwd' | 'gksphone' | 'yseries' | '17mov_Phone'
Config.Notifications = 'auto'   -- 'auto' | 'ox_lib' | 'okokNotify' | 'ps-ui' | 'lation_ui' | 'nox_notify'
Config.Locale        = 'en'
Config.Debug         = false
```

## App Registration

Shown inside the phone app drawer / launcher. Used to register against `lb-phone`, `yseries`, `gksphone`, `qs-smartphone(-pro)`, `17mov_Phone`. Change to rebrand.

```lua
Config.App = {
    name        = 'Banking',
    description = 'Mobile access to your bank accounts',
    icon        = 'https://cfx-nui-pc-banking/assets/brand.png',
}
```

| Field | Notes |
|-------|-------|
| `name` | App label shown on the home screen |
| `description` | App-store-style description (some phone resources show this on long-press) |
| `icon` | App icon URL — supports `cfx-nui-<resource>/<path>` and standard http(s) |

## Phone Auth

Phone-only auth tuning. Mirrors `Config.TwoFactor*` from pc-banking. Tune here without touching pc-banking.

```lua
Config.PhoneAuth = {
    sessionDurationHours = 24,    -- "remember me" lifetime for phone-app sessions; 0 = until disconnect
    twoFactorEnabled     = true,  -- respects per-profile two_factor_enabled flag
    twoFactorOTPExpiry   = 300,   -- seconds OTP is valid
    twoFactorCooldown    = 30,    -- seconds between OTP requests
    twoFactorMaxAttempts = 3,
}
```

## SMS / Mail Sender

The "from" identity used when the selected phone routes SMS or mail by phone number / email address (e.g. `yseries` requires a `from` number). Cosmetic — any string works.

```lua
Config.BankSmsNumber         = '611-BANK'
Config.BankMailSender        = 'noreply@lsbanking.gov'
Config.BankMailSenderDisplay = 'Los Santos Banking'
```

| Field | Used By |
|-------|---------|
| `BankSmsNumber` | SMS sender displayed in the phone messages app |
| `BankMailSender` | Mail "from" address |
| `BankMailSenderDisplay` | Mail "from" name |

## Locales

```lua
-- pc-banking-phone/locales/<lang>.lua
```

Locale tables are populated by `pc-banking-phone/locales/*.lua` (loaded before `bridge/main.lua`). Every string in the phone UI lives in a locale file and is shipped to the browser once on app boot via `pc-banking-phone:srv:getLocale`.

10 locales ship by default: `en`, `es`, `fr`, `de`, `it`, `pt`, `sv`, `ja`, `cn`, `ar`.

## DB Sharing

`pc-banking-phone` reads/writes the same `pc_banking_*` tables as `pc-banking`. The phone aggregates banking data across banks via its own server-side queries — there's no cross-resource RPC.

{% hint style="info" %}
Both resources MUST be loaded for cross-bank phone features (multi-bank account switcher, unified inbox, push notifications) to work end-to-end.
{% endhint %}
