# Oil Leak & Engine Seizure

Bottom of `pc-mechanic/config/ServicingDamage.lua`. Three chained systems: oil leaks, low-oil shutdowns, and engine seizure.

## Oil Leak System

```lua
Config.EnableOilLeakSystem = true

Config.OilLeakChanceOnDamage = {
    light    = 5,     -- 5% chance on light damage
    moderate = 30,    -- 30% chance on moderate
    severe   = 90     -- 90% chance on severe
}

Config.NotifyOnOilLeak       = true
Config.OilDecalInterval      = 500    -- ms between oil puddles
Config.OilDecalSize          = 2.0    -- puddle size
Config.OilDecalTimeout       = 120.0  -- puddle fade time (seconds)
Config.OilLeakDrainTimeSeconds = 360  -- time for oil to drain 100% → 0%
```

| Field | Purpose |
|-------|---------|
| `EnableOilLeakSystem` | Master switch for leaks (combustion only) |
| `OilLeakChanceOnDamage` | Rolled per damage event, severity-bucketed |
| `NotifyOnOilLeak` | Notify driver when a leak starts |
| `OilDecalInterval` | How often a puddle decal is dropped during a leak (ms) |
| `OilDecalSize` | Size of each decal |
| `OilDecalTimeout` | Decal fade time in seconds |
| `OilLeakDrainTimeSeconds` | Total drain duration from current oil % to 0 |

The leak chance is rolled **once per damage event**, using the same severity bucket the damage system computed. The chance ladder (5% / 30% / 90%) means light bumps almost never leak, severe crashes almost always do.

When a leak starts:
- Engine oil drains continuously to 0 over `OilLeakDrainTimeSeconds` regardless of driving
- Puddle decals drop on the road every `OilDecalInterval` ms while the vehicle is in motion
- Decals expire after `OilDecalTimeout` seconds

## Repairing a Leak

The repair item is configured in the items section:

```lua
Config.OilLeakRepairItem        = "blowtorch"
Config.OilLeakRepairItemRemove  = false       -- do not consume on use
Config.OilLeakRepairMechanicOnly = true       -- only mechanics can repair
```

A mechanic with the configured item walks up and seals the leak. Default is a reusable blowtorch — set `OilLeakRepairItemRemove = true` if you want it consumable.

## Low-Oil Shutdown System

Engine oil approaching empty triggers shutdowns:

```lua
Config.EngineOilShutdownThreshold = 10        -- start monitoring below 10%
Config.EngineOilMinTemp           = 90.0      -- normal engine temp °C
Config.EngineOilMaxTempIncrease   = 20.0      -- max temp gain at 0% oil

Config.MaxEngineOilShutdownChance  = 5        -- max shutdown chance % at 0%
Config.ZeroOilCheckIntervalMin     = 10000    -- min ms between checks
Config.ZeroOilCheckIntervalMax     = 15000    -- max ms between checks
Config.EngineHealthDegradePerShutdown = 10    -- engine health lost per shutdown
```

| Field | Purpose |
|-------|---------|
| `EngineOilShutdownThreshold` | Below this oil %, the system starts monitoring |
| `EngineOilMinTemp` | Baseline engine temperature |
| `EngineOilMaxTempIncrease` | How much hotter the engine runs at 0% oil |
| `MaxEngineOilShutdownChance` | Peak shutdown chance (rolled at each check) |
| `ZeroOilCheckIntervalMin/Max` | Random time between shutdown rolls |
| `EngineHealthDegradePerShutdown` | Health damage per shutdown — feeds back into damage system |

The shutdown chance scales linearly: at 10% oil, chance is near zero; at 0% oil, chance is `MaxEngineOilShutdownChance` (5% per check). With a 10-15 second roll interval and 5% chance, a 0% oil engine shuts down on average every ~4 minutes. Each shutdown removes 10 engine health, which may then trigger more damage-based degradation.

Topping up oil above the threshold stops monitoring immediately.

## Engine Seizure

```lua
Config.EnableEngineFireAt0Oil          = true
Config.EnableEngineSeizureAt0Oil       = true
Config.MinTimeBeforeSeizureSeconds     = 10
Config.MaxTimeBeforeSeizureSeconds     = 20
```

`EnableEngineFireAt0Oil` is the master toggle for zero-oil engine damage, seizure, and fire behavior. It defaults to `true`; set it to `false` to disable that entire behavior.

When oil reaches 0% (and the master toggle is on), the engine seizes after a random delay between min and max. A seized engine:

- Won't start
- Cannot be repaired with the standard repair kit
- Cannot be revived by adding oil
- Requires the **Engine Replacement** tuning option (`engine_replacement` item, `requiresSeizedEngine = true` in `Config.Tuning`)

Set `EnableEngineSeizureAt0Oil = false` if you want low oil to be permanently survivable — shutdowns continue but seizure never happens.

## Spark Plug / EV Battery Shutdowns

```lua
Config.EnableRandomShutdowns = true
Config.ShutdownThreshold     = 10        -- % at which shutdowns start
Config.MinShutdownDuration   = 5         -- seconds at threshold
Config.MaxShutdownDuration   = 30        -- seconds near 0
```

Separate from the oil shutdown system. Applies to **spark plugs** (combustion) and **EV battery** (electric):

| Vehicle | Triggering part |
|---------|-----------------|
| Combustion | Spark plugs below `ShutdownThreshold` |
| Electric | EV battery below `ShutdownThreshold` |

Shutdown duration scales with how low the part is — at 10% the duration is near `MinShutdownDuration`; at 0% it approaches `MaxShutdownDuration`. The shutdowns interrupt the engine for those seconds and resume.

Unlike the oil shutdown system, this one **does not** chip engine health and **does not** trigger seizure. It's a pure inconvenience layer until the part is replaced.

## Interactions

### Damage → Leak → Drain → Shutdown → Seizure (combustion)

```
Crash (severe) → 90% chance leak → 6 minutes drain to 0% → shutdowns + temp rise + health loss → seizure (10-20s after 0%)
```

Every link is independent and toggleable:
- Disable leak: `EnableOilLeakSystem = false` — drain stops happening on crash
- Disable seizure: `EnableEngineSeizureAt0Oil = false` — chain caps at shutdowns
- Disable shutdowns: lower `MaxEngineOilShutdownChance` to 0
- Disable spark/battery shutdowns: `EnableRandomShutdowns = false`

### Tyre Burst Tracking

```lua
Config.TrackTireBursts      = true
Config.TireBurstDegradation = 3   -- flat % loss on burst
```

Tyre bursts are tracked separately. The burst tyre takes a flat 3% on top of any `wheelBurst` rates configured per part. See [Damage System](damage-system.md) for how `wheelBurst` rates flow.
