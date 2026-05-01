# Resource Detection

**Clothing System Auto-Detection**

```lua
-- bridge.lua:128-138
if GetResourceState('illenium-appearance') == 'started' then
    -- Use illenium-appearance events
else
    -- Use default framework clothing
end
```

• **Inventory System Detection**

```lua
-- server/main.lua:61-69
if GetResourceState('qb-inventory') == 'started' then
    exports['qb-inventory']:AddItem(...)
elseif GetResourceState('ox_inventory') == 'started' then
    exports.ox_inventory:AddItem(...)
else
    -- Fallback to framework default
end
```

• **Spawn System Detection**

```lua
-- bridge.lua:294-313
-- Priority order: qbx_spawn > qb-spawn > um-spawn > renzu_spawn > default
```

• **Apartment System Detection**

```lua
-- bridge.lua:316-334
-- Priority: qb-apartments > qbx_properties > 0r-apartment-v2 > qs-apartments
```
