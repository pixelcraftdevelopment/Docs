# Prop Models

`pc-mechanic/config/Props.lua` selects the GTA prop models used by mechanic interactions.

```lua
Config.SprayProp   = "prop_paint_spray01a"
Config.engineModel = "prop_car_engine_01"
Config.HoistModel  = "xs_prop_x18_engine_hoist_02a"
Config.TabletModel = "prop_cs_tablet"
```

| Field | Purpose |
|-------|---------|
| `SprayProp` | Spray-can prop used during paint and respray actions |
| `engineModel` | Engine prop used during engine replacement |
| `HoistModel` | Engine-hoist prop used during engine replacement |
| `TabletModel` | Tablet prop displayed while using the mechanic tablet |

Use valid GTA prop model names. Restart `pc-mechanic` after changing a model.
