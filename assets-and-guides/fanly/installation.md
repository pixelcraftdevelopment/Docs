# Installation

## Prerequisites

* `ox_lib` (required — used for callbacks and notifications)
* `oxmysql` (required)
* QBCore, Qbox, or ESX framework
* MySQL 5.7+ / MariaDB 10.3+
* Any supported phone resource — lb-phone, yseries, gksphone, qs-smartphone, qs-smartphone-pro, qb-phone, 17mov_Phone, or npwd

## Steps

1. **Download** Fanly from FiveM keymaster (or your purchase source).
2. **Extract** to `resources/[apps]/fanly` (or any folder your `server.cfg` already loads).
3. **Database** — run `fanly/sql/fanly_install.sql` against your MySQL database. Creates all required tables on a fresh install (`IF NOT EXISTS` — safe to re-run).
4. **server.cfg** — add the ensure line **after** your framework, ox_lib, oxmysql, and your phone resource:

```
ensure ox_lib
ensure oxmysql
ensure qb-core               # or es_extended / qbx_core
ensure lb-phone              # or yseries / gksphone / qs-smartphone / qb-phone / 17mov_Phone / npwd

ensure fanly
```

5. **Start the server.** The Fanly app appears inside the phone's app launcher automatically.

{% hint style="success" %}
That's the full install. No extra configuration is needed for default behavior.
{% endhint %}

## First Run

* The Fanly icon shows up in the phone launcher on the first connect after install.
* Players tap to open and are taken to a Welcome screen, then sign-up or sign-in.
* No accounts exist until a player creates one — there is no migration.

## Optional: Banking Integration

By default, Fanly auto-detects an installed banking resource and uses it for all charges and payouts. Supported probes (priority order):

`pc-banking → qb-banking → okokBanking → Renewed-Banking → wasabi_banking → jaksam_billing → fd_banking → tgg-banking → crm-banking → prism_banking → p_banking → justbanks → RxBanking → esx_addonaccount → framework-native → internal`

If none of those are running, Fanly falls back to its own internal `fanly_wallet` table — fully standalone, useful for testing.

To force a specific provider, edit `fanly/config.lua`:

```lua
Config.Banking = 'pc-banking'    -- or 'qb-banking' / 'okokBanking' / 'native' / 'internal' / etc.
```

See [Banking Integration](configuration/banking.md) for the full list.

## Optional: Brand & Locale

* **Locale** — set `Config.Locale` in `fanly/config.lua` to one of `en, es, fr, de, it, pt, sv, ja, cn, ar`.
* **Branding** — change `Config.App.name`, `Config.App.description`, `Config.App.icon`, `Config.SmsSender`, `Config.MailSender` to rebrand the app for your server.

## Building the UI (developers only)

The shipped resource includes a pre-built UI in `ui/dist/`. You only need to rebuild if you want to modify Vue source files:

```
cd fanly/ui
npm install
npm run build
```

The build emits to `ui/dist/`. Restart the resource to pick up the new bundle.
