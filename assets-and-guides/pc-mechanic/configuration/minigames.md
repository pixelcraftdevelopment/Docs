# Minigames & Skillchecks

```lua
Config.UseExternalMinigames = true
Config.UseSkillbars         = true
Config.ProgressBarDuration  = 10000
Config.maxMiniGameAttempts  = 3
Config.MiniGameDifficulty   = { "easy", "easy", "easy", "easy", "easy" }
Config.MiniGameKeys         = { "w", "a", "s", "d" }
```

| Field | Purpose |
|-------|---------|
| `UseExternalMinigames` | When true, inspection minigames (OBD, pressure, multimeter, tread) use `pc-mechanic-minigames`. When false, internal fallbacks are used |
| `UseSkillbars` | Enable skill-bar style minigames (timing-based) |
| `ProgressBarDuration` | Default progress bar duration in ms |
| `maxMiniGameAttempts` | Max attempts at a minigame before failing the action outright |
| `MiniGameDifficulty` | Array of difficulty levels for sequential rounds. Length determines round count |
| `MiniGameKeys` | Keys eligible for press-prompt minigames |

## External vs Internal Minigames

Two layers of choice for inspection minigames:

1. **Global** — `Config.UseExternalMinigames` (boolean)
2. **Per-minigame** — each entry in `Config.InspectionMinigames` has a `useExternal` field:
   - `"default"` — defer to the global setting
   - `"yes"` — always use external (`pc-mechanic-minigames`)
   - `"no"` — always use internal

This lets you mix and match. Use external for the polished pressure and multimeter minigames but stick to internal for OBD, for example.

## Skillbar Behavior

```lua
Config.UseSkillbars = true
Config.MiniGameDifficulty = { "easy", "easy", "easy", "easy", "easy" }
Config.MiniGameKeys       = { "w", "a", "s", "d" }
```

When `UseSkillbars = true`, modifications, servicing, and other actions that require a successful timing minigame use the configured skillcheck system (`Config.SkillCheck`):

- Each entry in `MiniGameDifficulty` is one round of the skillbar
- `MiniGameKeys` are which keys can be the prompt
- Difficulty values: `"easy"`, `"medium"`, `"hard"`, `"very_hard"` (depending on skillcheck system)

Adjust round count by changing the array length:

```lua
-- Three rounds
Config.MiniGameDifficulty = { "easy", "medium", "hard" }
```

## Max Attempts

```lua
Config.maxMiniGameAttempts = 3
```

How many tries a player gets before the action fails outright. Failed action means:

- For modifications: the cart item may be consumed without effect (depending on shop config) — players take a real loss
- For servicing: the service doesn't apply, item not consumed
- For inspection: result is unknown / shown as inconclusive

Setting this to 1 makes minigames brutal; raising to 5 makes them forgiving.

## Progress Bar

```lua
Config.ProgressBarDuration = 10000
```

Default progress bar duration in milliseconds (10 seconds). Used as a cap for installation, service, and inspection animations. Specific actions may override this internally for shorter operations.
