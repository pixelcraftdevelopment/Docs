# Subscription Intervals & Auto-Renew

Controls how long each subscription tier lasts and which tiers automatically renew.

## Time Convention

All intervals use a compact string format: `<N><unit>` — units are `S` (seconds), `M` (minutes), `H` (hours), `D` (days), `W` (weeks). Examples: `'30S'`, `'1M'`, `'2H'`, `'7D'`, `'4W'`.

Defaults follow the **game-time convention** that matches `pc-banking`:

* 7 real days = 1 in-game month
* 84 real days (7 × 12) = 1 in-game year

## Renewer Cadence

How often the background renewer wakes up to process auto-renewals.

```lua
Config.SubscriptionCheckInterval = '1M'   -- once per real minute
```

Keep this `<=` the shortest subscription interval, otherwise renewals will lag behind the configured cycle.

## Subscription Term Lengths

How long each tier lasts after a successful charge.

```lua
Config.SubscriptionIntervals = {
    monthly   = '7D',    -- 1 in-game month
    bundle_3  = '21D',   -- 3 in-game months
    bundle_6  = '42D',   -- 6 in-game months
    bundle_12 = '84D',   -- 12 in-game months / 1 in-game year
}
```

To switch to real-time:

```lua
Config.SubscriptionIntervals = {
    monthly   = '30D',
    bundle_3  = '90D',
    bundle_6  = '180D',
    bundle_12 = '365D',
}
```

To accelerate for testing:

```lua
Config.SubscriptionIntervals = {
    monthly   = '5M',
    bundle_3  = '15M',
    bundle_6  = '30M',
    bundle_12 = '60M',
}
Config.SubscriptionCheckInterval = '30S'
```

## Auto-Renew Toggles

Which tiers actually auto-renew when their term ends.

```lua
Config.SubscriptionAutoRenew = {
    monthly   = true,
    bundle_3  = true,
    bundle_6  = true,
    bundle_12 = true,
    trial     = false,    -- trials never auto-renew
}
```

By default, **monthly** renews. The OnlyFans-style design treats bundles and trials as one-shot purchases — fans actively resubscribe when they end. You can flip any of these to change the model:

* `monthly = false` — even monthly subs become one-shot purchases.
* `bundle_X = true` — bundles auto-renew at the end of their term.

{% hint style="warning" %}
Trials should stay `false`. Auto-renewing a trial would silently start charging the fan when their trial ends — bad user experience and a source of refund disputes.
{% endhint %}

## Legacy Fallback

```lua
Config.RenewerIntervalSec = 300   -- 5 minutes
```

Older configs that don't set `Config.SubscriptionCheckInterval` fall back to this seconds value. New installs should tune `SubscriptionCheckInterval` instead.
