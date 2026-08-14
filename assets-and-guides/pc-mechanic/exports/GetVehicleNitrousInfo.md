# GetVehicleNitrousInfo

Returns the current nitrous status for the local player's vehicle or for a vehicle plate.

```lua
exports['pc-mechanic']:GetVehicleNitrousInfo(plate)
```

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `plate` | string | No | Vehicle plate to look up. Omit it to read the local player's current vehicle. |

## Returns

Returns `false` when no vehicle can be resolved. Otherwise it returns this table:

| Field | Type | Description |
|-------|------|-------------|
| `plate` | string \| nil | Normalized vehicle plate. |
| `live` | boolean | `true` when the information was read from the local vehicle's live state; `false` when it was retrieved from stored data. |
| `installed` | boolean | `true` when at least one nitrous bottle is installed. |
| `installedBottles` | number | Total installed bottles. |
| `filledBottles` | number | Fully filled bottles, excluding an in-use partial bottle. |
| `emptyBottles` | number | Installed bottles with no nitrous remaining. |
| `bottleLevels` | number[] | Per-bottle fill percentages, ordered by bottle index. |
| `activeBottleLevel` | number | Fill percentage of the partially used bottle; `0` when no partial bottle is active. |
| `capacityPerBottle` | number | Boost seconds supplied by one full bottle (`Config.BoostTime`). |
| `remainingBoostSeconds` | number | Total boost time remaining across all bottles. |
| `maximumBoostSeconds` | number | Total boost time when every installed bottle is full. |
| `remainingPercent` | number | Total remaining nitrous as a percentage of maximum capacity. |
| `maxBottles` | number | Installation limit from `Config.BoostMaxBottle`. |
| `isBoosting` | boolean | `true` while nitrous boost is active. |
| `isPurging` | boolean | `true` while nitrous purge is active. |
| `onCooldown` | boolean | `true` while boost cannot be used because its cooldown is active. |
| `isEmpty` | boolean | `true` when no boost seconds remain. |
| `needsRefill` | boolean | `true` when bottles are installed but total capacity is not full. |
| `canInstallMore` | boolean | `true` when the installed bottle count is below `maxBottles`. |

```lua
local info = exports['pc-mechanic']:GetVehicleNitrousInfo('PCMECH')

if info then
    print(('Nitrous: %.0f%% remaining'):format(info.remainingPercent))
end
```

This is a client export. When the requested vehicle is not the local player's current vehicle, PC-Mechanic retrieves its stored nitrous data by plate.
