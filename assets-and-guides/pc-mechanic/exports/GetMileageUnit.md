# GetMileageUnit

**Side:** Client

Returns the configured mileage unit string.

## Signature

```lua
exports['pc-mechanic']:GetMileageUnit()
```

## Returns

`string` — `"kilometers"` or `"miles"`, matching `Config.MileageUnit`.

## Example

```lua
local mileage = exports['pc-mechanic']:GetVehicleMileage(vehicle)
local unit    = exports['pc-mechanic']:GetMileageUnit()
print(('Odometer: %d %s'):format(mileage, unit))
```
