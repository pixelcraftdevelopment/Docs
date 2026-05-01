# Garage

The garage system integration is primarily for QBCore houses.

**Configuration Location**

**server/main.lua (lines 74-112):**

```lua
local function loadHouseData(src)
    if Bridge.Framework ~= 'QBCORE' then
        return
    end
    -- Skip house data loading for qbx as it uses qbx_properties
    if Bridge.IsQbox or GetResourceState('qbx_properties') == 'started' then
        return
    end
    -- ... house loading logic ...
    if Bridge.Framework == 'QBCORE' then
        TriggerClientEvent("qb-garages:client:houseGarageConfig", src, HouseGarages)
        TriggerClientEvent("qb-houses:client:setHouseConfig", src, Houses)
    end
end
```

**Customizing Garage Integration**

1. **Change garage events** (line 109):

```lua
TriggerClientEvent("your-garages:client:houseGarageConfig", src, HouseGarages)
```

2. **Modify garage data structure** (lines 102-105):

```lua
HouseGarages[v.name] = {
    label = v.label,
    takeVehicle = garage,
    -- Add custom fields
    parkingSpots = v.parkingSpots,
    vehicleLimit = v.vehicleLimit
}
```
