# Standing Orders

Recurring payment scheduler controls in `pc-banking/config/config.lua`.

```lua
Config.StandingOrders = {
    enabled                = true,
    maxFailuresBeforePause = 3,
    notifyOnExecution      = true,
    notifyOnFailure        = true,
    notifyBeforeEMI        = true,
}
```

## Field Reference

| Field | Type | Behavior |
|-------|------|----------|
| `enabled` | bool | Master gate for standing-order create/update/processing paths. |
| `maxFailuresBeforePause` | number | Consecutive failures before order auto-pauses. |
| `notifyOnExecution` | bool | Sends success notification when an order executes. |
| `notifyOnFailure` | bool | Sends failure notifications for execution failures. |
| `notifyBeforeEMI` | bool | Enables pre-run reminder notifications for upcoming orders. |

## Reminder Behavior (`notifyBeforeEMI`)

When enabled, runtime sends up to 3 reminder tiers per cycle based on elapsed cycle window (`cycle_start -> next_run`). Reminder progress is tracked by `reminders_sent` and reset after execution.

## Scheduler Interval

```lua
Config.StandingOrderCheckInterval = '1M'
```

This controls how often the standing-order scheduler wakes and processes due/reminder logic.
