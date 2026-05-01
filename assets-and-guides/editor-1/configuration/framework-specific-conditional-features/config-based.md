# Config Based

_Skip Selection Mode_\*

```lua
-- config.lua
Config.SkipSelection = false -- Auto-select if one character

-- server/main.lua:200-203
if Config.SkipSelection then
    -- Spawn directly at last location
else
    -- Show spawn selection UI
end
```

• **Delete Button Toggle**

```lua
-- config.lua
Config.EnableDeleteButton = true

-- server/main.lua:456-458
if not Config.EnableDeleteButton then 
    return -- Prevent deletion
end
```

• **Nationality Field Type**

```lua
-- config.lua
Config.customNationality = false
-- false: Dropdown selection
-- true: Text input field
```
