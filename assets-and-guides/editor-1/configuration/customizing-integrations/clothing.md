# Clothing

PC-Multicharacter supports multiple clothing systems. The detection and configuration is handled in **bridge.lua**.

**Supported Clothing Systems**

1. **illenium-appearance** (auto-detected)
2. **qb-clothing** (default for QBCore)
3. **qb-clothes** (alternative QBCore)
4. **esx\_skin** (default for ESX)

**Configuration Locations**

**bridge.lua (lines 126-138):**

```lua
-- Clothing events
Bridge.ClothingEvents = {}
if GetResourceState('illenium-appearance') == 'started' then
    -- illenium-appearance uses same events for both frameworks
    Bridge.ClothingEvents.createFirst = Bridge.Framework == 'ESX' and 'esx_skin:openSaveableMenu' or 'qb-clothing:client:openMenu'
    Bridge.ClothingEvents.openMenu = Bridge.Framework == 'ESX' and 'esx_skin:openSaveableMenu' or 'qb-clothing:client:openMenu'
    Bridge.ClothingEvents.loadPlayerClothing = Bridge.Framework == 'ESX' and 'skinchanger:loadSkin' or 'qb-clothing:client:loadPlayerClothing'
else
    -- Default clothing events
    Bridge.ClothingEvents.createFirst = Bridge.Framework == 'ESX' and 'esx_skin:openSaveableMenu' or 'qb-clothes:client:CreateFirstCharacter'
    Bridge.ClothingEvents.openMenu = Bridge.Framework == 'ESX' and 'esx_skin:openSaveableMenu' or 'qb-clothing:client:openMenu'
    Bridge.ClothingEvents.loadPlayerClothing = Bridge.Framework == 'ESX' and 'esx_skin:loadSkin' or 'qb-clothing:client:loadPlayerClothing'
end
```

**Adding Custom Clothing System**

To add a custom clothing system, modify the clothing events in **bridge.lua**:

1. **Add detection** (after line 128):

```lua
elseif GetResourceState('your-clothing-resource') == 'started' then
    Bridge.ClothingEvents.createFirst = 'your-clothing:firstCharacter'
    Bridge.ClothingEvents.openMenu = 'your-clothing:openMenu'
    Bridge.ClothingEvents.loadPlayerClothing = 'your-clothing:loadClothing'
```

2. **Modify ApplyClothing function** (lines 141-285):

```lua
-- Add after line 150
elseif GetResourceState('your-clothing-resource') == 'started' then
    exports['your-clothing-resource']:ApplyClothingToPed(ped, skinData)
    return
```

3. **Update skin loading** in **server/main.lua** (lines 529-540):

```lua
-- For custom skin table structure
local result = MySQL.query.await('SELECT skin FROM your_skin_table WHERE identifier = ?', {citizenid})
```
