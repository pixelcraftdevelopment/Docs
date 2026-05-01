# Spawn Priority Logic

**For Existing Characters:**

```lua
-- QBCore Priority:
1. um-spawn (if detected)
2. renzu_spawn (if detected)
3. qb-spawn/qbx_spawn (default)

-- ESX Priority:
1. Config.ESX.SpawnResource (if configured)
2. Config.ESX.ApartmentResource (if configured)
3. Last position spawn (fallback)
```

2.  **For New Characters:**

    ```lua
    -- QBCore:
    if Bridge.ApartmentSystem.type ~= 'none' then
        -- Apartment UI
    else
        -- Spawn selection UI
    end

    -- ESX:
    -- Same priority as existing characters
    ```
