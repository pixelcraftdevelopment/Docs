# Pricing Guard Rails

Server-enforced minimum / maximum bounds on every price creators can set. The UI also enforces these so creators can't even type out-of-range values.

```lua
Config.Pricing = {
    minMonthly       = 5,
    maxMonthly       = 500,
    minTip           = 1,
    maxTip           = 5000,
    minPPV           = 1,
    maxPPV           = 500,
    maxBundleOffPct  = 60,
    maxBundle3OffPct  = 60,
    maxBundle6OffPct  = 60,
    maxBundle12OffPct = 60,
    maxTrialDays    = 30,
    maxPromoPct     = 60,
}
```

## Subscription Pricing

| Key | What | Default |
|-----|------|---------|
| `minMonthly` | Lowest base monthly price a creator can set | 5 |
| `maxMonthly` | Highest base monthly price | 500 |

## Tips

| Key | What | Default |
|-----|------|---------|
| `minTip` | Smallest tip a fan can send | 1 |
| `maxTip` | Largest tip a fan can send | 5000 |

## Pay-Per-View

| Key | What | Default |
|-----|------|---------|
| `minPPV` | Lowest per-post unlock price | 1 |
| `maxPPV` | Highest per-post unlock price | 500 |

## Bundle Discounts

Bundles are prepaid 3 / 6 / 12-month subscriptions sold at a discount off the base monthly rate.

| Key | What | Default |
|-----|------|---------|
| `maxBundleOffPct` | Legacy single-cap fallback for any per-bundle key left unset | 60 |
| `maxBundle3OffPct` | Max % off allowed on the 3-month bundle | 60 |
| `maxBundle6OffPct` | Max % off allowed on the 6-month bundle | 60 |
| `maxBundle12OffPct` | Max % off allowed on the 12-month bundle | 60 |

You can step the caps to reward longer commitment:

```lua
Config.Pricing.maxBundle3OffPct  = 50   -- 3-month max 50% off
Config.Pricing.maxBundle6OffPct  = 65   -- 6-month max 65% off
Config.Pricing.maxBundle12OffPct = 80   -- 12-month max 80% off
```

## Trials

| Key | What | Default |
|-----|------|---------|
| `maxTrialDays` | Longest trial a creator can offer | 30 |

## Promos

| Key | What | Default |
|-----|------|---------|
| `maxPromoPct` | Max % off on a first-month promo | 60 |
