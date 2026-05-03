# Discord Webhooks

```lua
Config.DiscordWebhooks = {
    ImageUrl            = "https://forum.cfx.re/user_avatar/forum.cfx.re/pixelcraft_dev/48/5087487_2.png",
    WorkOrdersLog       = "",
    ServiceLog          = "",
    BillingLog          = "",
    StaffManagementLog  = ""
}
```

| Field | Purpose |
|-------|---------|
| `ImageUrl` | Avatar shown in Discord for webhook posts |
| `WorkOrdersLog` | Webhook URL for work order events (created, claimed, completed, deleted) |
| `ServiceLog` | Webhook URL for servicing events (oil changes, tyre swaps, inspections) |
| `BillingLog` | Webhook URL for invoice events (sent, paid, refunded) |
| `StaffManagementLog` | Webhook URL for staff events (hired, fired, promoted, demoted) |

## Setup

1. In your Discord server, create a webhook for each channel you want logs in (Server Settings → Integrations → Webhooks → New Webhook).
2. Copy the webhook URL.
3. Paste it into the matching field. Empty strings disable that log channel.

## Recommended Channel Layout

A typical setup uses three or four channels:

- `#mech-orders` ← `WorkOrdersLog` — track shop output, see when orders pile up
- `#mech-service` ← `ServiceLog` — visibility on inspection/replacement work
- `#mech-billing` ← `BillingLog` — finance trail
- `#mech-staff` ← `StaffManagementLog` — hire/fire trail, useful for owners auditing managers

## What Gets Logged

Each webhook posts structured embeds with timestamp, employee name, target (vehicle plate, customer), action, and amount/details where relevant. The image avatar (`ImageUrl`) appears next to every post.

## Privacy

These webhooks send player names, character IDs, vehicle plates, and amounts to Discord. If your server has player privacy concerns, leave the URLs empty or post to a staff-only channel.
