# Exports

Public exports for vendor/integration scripts. Use from other resources via `exports['pc-mechanic'].FunctionName(...)`.

## Vehicle Properties

* [getmods](getmods.md) — read full vehicle properties (with statebag data)
* [setmods](setmods.md) — apply vehicle properties to an entity

## Mileage

* [GetVehicleMileage](GetVehicleMileage.md) — read current mileage by entity
* [GetMileageUnit](GetMileageUnit.md) — read configured unit (`"kilometers"` / `"miles"`)

## Tuning & Handling

* [getTuningHandlingModifiers](getTuningHandlingModifiers.md) — compute handling deltas from a tuning config
* [getServicingHandlingModifiers](getServicingHandlingModifiers.md) — compute handling deltas from servicing health
* [applyHandlingTuning](applyHandlingTuning.md) — apply tuning handling to a vehicle entity
