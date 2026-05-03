# Stance

```lua
Config.StanceMinSuspensionHeight = -0.3
Config.StanceMaxSuspensionHeight = 0.3
Config.StanceMinCamber           = 0.0
Config.StanceMaxCamber           = 0.5
Config.StanceMinTrackWidth       = 0.5
Config.StanceMaxTrackWidth       = 1.25

Config.StanceNearbyVehiclesFreqMs        = 500
Config.TuningGiveInstalledItemBackOnRemoval = false
```

| Field | Purpose |
|-------|---------|
| `StanceMinSuspensionHeight` / `Max` | Vertical offset clamp. Negative lowers the body, positive raises it |
| `StanceMinCamber` / `Max` | Camber angle range in radians. 0 = wheels vertical, 0.5 ≈ 28° tilt at the top |
| `StanceMinTrackWidth` / `Max` | Wheel poke clamp. 1.0 = stock, lower brings wheels in, higher pushes them out |
| `StanceNearbyVehiclesFreqMs` | Nearby vehicle scan interval while stance UI is open. Used for visualizing other cars at the same time |
| `TuningGiveInstalledItemBackOnRemoval` | When uninstalling a tuning option, return the original item to inventory (`true`) or consume it forever (`false`) |

## Item Required

Stance requires the configured item from `Config.Mods.ItemsRequired.stance` (default `stancing_kit`). With `removeItem = false`, the kit is **reusable** — adjust your stance unlimited times without consuming the item.

## Clamps

The clamps are hard limits. Anything beyond them is rejected, regardless of UI input. This prevents:

- Wheels poking through bodywork (track width too high)
- Wheels disappearing inside the chassis (track width too low)
- Bumper scraping the ground (suspension too low)
- Wheels under the body (suspension too high)

If you want wider stance ranges (e.g. for a custom MLO with wide bays), expand the clamps in config and restart.

## Item Return on Removal

`TuningGiveInstalledItemBackOnRemoval` applies to **tuning** removal, not stance. Stance is reset by simply re-adjusting; there's no "removal." For tuning options (engines, drivetrains, etc.), this knob decides whether removing the option puts the item back in inventory or just deletes it.

Default `false` makes installation one-way — you commit to the part. Set `true` if your server prefers reversible tuning where players can sell/trade removed parts.
