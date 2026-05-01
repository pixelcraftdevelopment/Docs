# QBCore-Specific

**House System Integration**

```lua
-- Only loads for QBCore, not Qbox
if Bridge.IsQbox or GetResourceState('qbx_properties') == 'started' then
    return -- Skip house loading
end
```

• **Command System**

```lua
-- server/main.lua:193-194
if Bridge.Framework == 'QBCORE' then
    Bridge.Core.Commands.Refresh(src)
end
```

• **Apartment Creation**

```lua
-- Different bucket handling for apartments
local randbucket = (GetPlayerPed(src) .. math.random(1,999))
SetPlayerRoutingBucket(src, randbucket)
```
