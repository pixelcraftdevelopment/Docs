# Discord Logging

## Discord Webhook Logging

PC Crafting integrates with Discord via webhooks for detailed server logging. Enable logging with `Config.EnablePcLogs = true` in `config.lua`. Each event type has its own configurable webhook URL.

![Discord Webhook Logs](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/Discord/1.png)

## Log Channels

Configure each webhook in `Config.DiscordWebhooks`:

- **ImageUrl:** Optional thumbnail/avatar image for all embeds
- **CraftingLog:** Logs all crafting completions and cancellations — who crafted what, when, and at which table
- **RepairLog:** Logs weapon repairs and attachment changes — includes item name, parts replaced, and player info
- **EconomyLog:** Logs item transfers to and from crafting tables — tracks material flow
- **TableLog:** Logs placeable table placement and pickup events — coordinates, player, and table type

## Setting Up Webhooks

1. In your Discord server, go to the desired channel's settings
2. Navigate to **Integrations → Webhooks → New Webhook**
3. Name the webhook (e.g. "PC Crafting - Crafting Log") and select the channel
4. Copy the webhook URL
5. Paste it into the appropriate field in `Config.DiscordWebhooks` in `config.lua`
6. Repeat for each log channel you want to activate
7. Restart the resource — logs begin flowing to Discord

> **Note:** Leave a webhook URL empty (`""`) to disable that specific log channel. You can use the same webhook for multiple channels if desired, but separate channels improve organization.
