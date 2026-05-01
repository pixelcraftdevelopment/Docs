# Scheduled Tasks & Intervals

Background timing values in `pc-banking/config/config.lua`.

## Accepted Interval Formats

- `'<N>S'` seconds
- `'<N>M'` minutes
- `'<N>H'` hours
- `'<N>D'` days
- `'<N>W'` weeks
- `'ingame'` special alias (treated as ~24 real hours in interval parser)

Examples: `'30S'`, `'5M'`, `'2H'`, `'7D'`, `'4W'`, `'84D'`, `'ingame'`.

## Scheduler Wake Intervals

```lua
Config.ScheduledTaskInterval      = '1M'
Config.CardCheckInterval          = '1M'
Config.StandingOrderCheckInterval = '1M'
```

## Economy Intervals

```lua
Config.InterestAccrualInterval = '7D'
Config.MonthlyFeeInterval      = '7D'
Config.AnnualFeeInterval       = '84D'
Config.CreditBillingInterval   = '7D'
Config.EMIInterval             = '7D'
Config.DefaultReminderInterval = '28D'
Config.DefaultWriteOffAfter    = '70D'
Config.LateScarDecayAfter      = '28D'
```

## Notes

1. Wake intervals should be shorter than or equal to the smallest job interval they service.
2. These values are consumed by scheduler/interval utilities in server runtime; malformed strings fall back to built-in defaults.
