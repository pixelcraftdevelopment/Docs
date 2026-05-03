# Damage System

Top of `pc-mechanic/config/ServicingDamage.lua`. Maps physical damage events (crashes, tyre bursts, rollovers) to wear on individual parts.

## Master Toggles

```lua
Config.EnableDamageBasedDegradation = true
Config.DamageDegradationDebug       = false
Config.DamageCheckInterval          = 500    -- ms (500 = 2 checks/sec)
```

| Field | Purpose |
|-------|---------|
| `EnableDamageBasedDegradation` | Master switch. If false, only mileage wears parts |
| `DamageDegradationDebug` | Print every damage event to console (development only) |
| `DamageCheckInterval` | How often the system samples body/engine health (in ms) |

Lowering `DamageCheckInterval` makes detection more responsive at higher CPU cost. 500 ms is a good balance.

## Damage Thresholds

```lua
Config.MinBodyDamage   = 20
Config.MinEngineDamage = 20
```

If a single sample shows less than this much health change, the event is ignored. Stops small bumps from grinding parts down.

## Severity Classification

```lua
Config.DamageSeverity = {
    light    = 80,
    moderate = 150,
    severe   = 250
}
```

Health change in a single sample is classified into one of three buckets:

| Bucket | Default health-loss range |
|--------|---------------------------|
| `light` | ≤ 80 |
| `moderate` | ≤ 150 |
| `severe` | ≤ 250 (and above) |

These thresholds are **inclusive upper bounds** for each bucket. So a 90-point hit is moderate, a 200-point hit is severe.

## Severity Multipliers

```lua
Config.SeverityMultipliers = {
    light    = 0.5,
    moderate = 1.0,
    severe   = 1.5
}
```

The base degradation calculation is multiplied by the severity bucket's multiplier. Light hits cause half the wear, severe hits cause 1.5×.

## Per-Part Degradation Rates

```lua
Config.DamageBasedDegradation = {
    suspension = { bodyDamage = 1.25, rollover = 2.5, wheelBurst = 1.5 },
    tyres      = { bodyDamage = 0.5,  wheelBurst = 4.0, rollover = 1.0 },
    brakePads  = { bodyDamage = 0.75, wheelBurst = 1.0 },
    engineOil  = { engineDamage = 2.5, bodyDamage = 1.5 },
    clutch     = { engineDamage = 1.0 },
    airFilter  = { engineDamage = 2.25, bodyDamage = 1.75 },
    sparkPlugs = { engineDamage = 2.0, bodyDamage = 1.25 },
    evMotor    = { engineDamage = 1.25, bodyDamage = 0.4 },
    evBattery  = { engineDamage = 1.0,  bodyDamage = 0.75, rollover = 1.5 },
    evCoolant  = { engineDamage = 1.25, bodyDamage = 0.5 }
}
```

Rates are "% degradation per 100 health points lost." Each part can list any subset of:

| Source | Triggered by |
|--------|-------------|
| `bodyDamage` | Body health decrease |
| `engineDamage` | Engine health decrease |
| `wheelBurst` | A tyre bursting |
| `rollover` | Vehicle flipped past `Config.RolloverThreshold` |

## Calculation

```
degradation% = (rate × healthLost / 100) × severityMultiplier
```

**Example:** A severe hit drops 250 body health on a combustion car:

| Part | Calculation | Result |
|------|-------------|--------|
| Engine Oil | 1.5 × 250/100 × 1.5 | 5.6% |
| Air Filter | 1.75 × 250/100 × 1.5 | 6.6% |
| Suspension | 1.25 × 250/100 × 1.5 | 4.7% |
| Tyres | 0.5 × 250/100 × 1.5 | 1.9% |

A separate calculation runs for engine damage. Each source is computed independently and applied to all listed parts.

## Rollover Detection

```lua
Config.RolloverThreshold = 90    -- degrees from upright
```

When a vehicle's roll exceeds this angle, the rollover damage column is triggered for every part with a `rollover` rate. A flipped car typically lands a single rollover event.

## Driver Notifications

```lua
Config.NotifyOnDamageDegradation     = true
Config.MinDegradationForNotification = 5    -- % loss minimum to notify
```

Only triggers a "your X is now at Y%" notification when the loss in a single event exceeds the minimum. Prevents notification spam from small dings.

## Tyre Burst Tracking

```lua
Config.TrackTireBursts        = true
Config.TireBurstDegradation   = 3       -- % instant loss on the burst tyre itself
```

Two separate effects of a tyre burst:

1. The **burst tyre itself** takes a flat instant loss (`TireBurstDegradation`).
2. **Every part with a `wheelBurst` rate** takes the calculated wear in addition.

So a tyre burst hits the bursting tyre with 3% (instantly) plus its `wheelBurst` rate (4 × severity), and also chips suspension (1.5 × severity) and brakes (1.0 × severity).

## Interactions

### With Mileage

Both systems run in parallel and write to the same condition % per part. Mileage is continuous; damage is event-driven. The two stack — the part wears from both sources independently.

### With Oil & Seizure

Body and engine damage simultaneously feed:

- The damage system (per-part wear via `engineOil` line: 2.5× engine + 1.5× body damage rates)
- The oil leak system (chance of leak rolled per severity)

A severe crash on a combustion car can trigger an oil leak (90% chance) **and** lose 5-7% of engine oil to wear in the same event. The leak then drains oil over time, eventually triggering shutdowns and seizure.

### With Combustion vs Electric

Combustion-only parts (`engineOil`, `clutch`, `airFilter`, `sparkPlugs`) only take damage on combustion vehicles. EV-only parts (`evMotor`, `evBattery`, `evCoolant`) only take damage on electric vehicles. The system reads the vehicle's electric status (auto-detected on game build 3258+, list-based on older builds) before applying.

### Tuning Down Damage

To reduce damage influence:
- Raise `MinBodyDamage` / `MinEngineDamage` to ignore small hits
- Reduce `SeverityMultipliers` (e.g. light: 0.25, moderate: 0.5, severe: 1.0)
- Reduce per-part rates in `DamageBasedDegradation`

To **disable** damage influence entirely: `Config.EnableDamageBasedDegradation = false`. Mileage wear continues normally.
