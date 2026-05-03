# Installation Mode

```lua
Config.InstallationMode = "sequential"   -- "individual" | "sequential" | "bulk"
```

Controls how multi-category mod work plays out as a UX. When a customer queues several categories at once (paint + wheels + body kit + neon), this setting decides how the mechanic walks through them.

| Mode | Behavior |
|------|----------|
| `individual` | One minigame per category. Mechanic confirms each step manually. Each step can succeed or fail independently |
| `sequential` | One continuous flow. All categories run one after another with a unified progress UI. Mechanic doesn't re-confirm between steps |
| `bulk` | A single minigame at the start. Pass once, all categories install. Fail once, none of them install |

## Trade-offs

| Concern | individual | sequential | bulk |
|---------|------------|------------|------|
| Time to complete a big work order | Slowest | Medium | Fastest |
| Risk of partial work | Low (each step succeeds/fails alone) | Low | High (single minigame can fail the entire cart) |
| Player friction | High (multiple confirms) | Low | Lowest |
| Mechanic skill expression | High | Medium | Single point of skill |

## Recommended Use

- **individual** — RP-heavy server where each step is its own meaningful action
- **sequential** — most servers; balance of speed and engagement
- **bulk** — fast-paced racing/casual servers where mod work is utility

## Interaction With Other Settings

- `Config.maxMiniGameAttempts` applies per round in `individual` and `sequential`. In `bulk`, the single minigame uses the same retry budget
- `Config.MiniGameDifficulty` array applies as configured regardless of mode
- Installation mode does **not** affect tuning installation (engines, drivetrains, etc.) — those are always individual due to the part requirement per category
