# ESX-Specific

**Spawn/Apartment Toggle**

```lua
-- server/main.lua:217-238
if Config.ESX.SpawnResource and GetResourceState(Config.ESX.SpawnResource) == 'started' then
    -- Use spawn resource
elseif Config.ESX.ApartmentResource and GetResourceState(Config.ESX.ApartmentResource) == 'started' then
    -- Use apartment resource
else
    -- Direct spawn at last location
end
```

• **Character Slot Format**

```lua
-- ESX uses: char1:license_hash
-- QBCore uses: citizenid (ABC12345)
```

• **Default Spawn Behavior**

```lua
-- ESX: Falls back to last position or Config.DefaultSpawn
-- QBCore: Always uses spawn selection unless Config.SkipSelection
```
