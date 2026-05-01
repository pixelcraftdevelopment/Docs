# Discord Webhooks

Webhook settings in `pc-banking/config/config.lua`.

```lua
Config.Webhooks = {
    transactions = '',
    security     = '',
    admin        = '',
}
Config.WebhookThreshold = 10000
```

## Field Reference

| Field | Type | Behavior |
|-------|------|----------|
| `Webhooks.transactions` | string | URL for transaction webhook channel. Empty string disables it. |
| `Webhooks.security` | string | URL for security webhook channel. Empty string disables it. |
| `Webhooks.admin` | string | URL for admin/system webhook channel. Empty string disables it. |
| `WebhookThreshold` | number | Amount threshold used by large-transfer transaction webhook path. |

## Current Event Usage

- `transactions`: large transfer events (amount `>= WebhookThreshold`)
- `security`: account creation and password-change security events
- `admin`: loan admin-style lifecycle events (approved/paid off/defaulted/written off)

Set `WebhookThreshold = 0` if you want all transfer amounts to qualify for the large-transfer webhook condition.
