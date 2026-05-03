# Queue & History

## Queue System

The Queue system lets multiple crafting jobs stack. When you start crafting an item, it enters the queue as "In Progress". Additional crafts go into "Pending" status and begin automatically when the current job completes.

The **Queue** tab displays all jobs with:

- **Name:** The item being crafted
- **Remaining Time:** Time left until this job completes
- **Start Time:** When the crafting started
- **End Time:** When the craft is expected to complete
- **Status:** `In Progress` or `Pending`

![Queue System](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/Queue/1.png)

## Queue Behavior

1. Start crafting an item — it enters the queue immediately as **In Progress** with a countdown timer
2. You can queue additional items while the first is crafting — they appear as **Pending**
3. You can close the crafting UI and the queue continues server-side
4. When a job completes, the item is delivered to your inventory and the next pending job starts automatically
5. Items in the queue are protected by the anti-spam system — a minimum delay between consecutive submissions prevents abuse

> **Note:** The queue is per-player. Each player has their own independent queue. Queue state is stored server-side.

## History Log

The **History** tab shows a log of all past crafting and repair operations performed in this session. Each entry records:

- **Item Name:** What was crafted or repaired
- **Action:** Craft or Repair
- **Timestamp:** When the operation completed
- **Result:** Success or failure

History is also logged server-side and sent to Discord webhooks if `Config.EnablePcLogs = true`. Helps admins monitor crafting activity and detect abuse.

## Anti-Spam Protection

The anti-spam system in `config.lua` prevents rapid submission of craft/repair requests:

- `Config.AntiSpamEnabled = true` — Enable/disable the system
- `Config.AntiSpamConsecutiveClicks = 5` — Number of consecutive actions before cooldown triggers
- `Config.AntiSpamCooldownTime = 5000` — Cooldown duration in milliseconds (5 seconds default)
