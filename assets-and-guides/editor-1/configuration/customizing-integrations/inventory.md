# Inventory

PC-Multicharacter supports multiple inventory systems for giving starter items.

**Supported Inventory Systems**

1. **qb-inventory** (auto-detected)
2. **ox\_inventory** (auto-detected)
3. **Default framework inventory** (fallback)

**Configuration Locations**

**bridge.lua (lines 760-795):**

```lua
function Bridge.AddItem(source, item, amount, slot, info)
        if GetResourceState('ox_inventory') == 'started' then
            local success, response = exports.ox_inventory:AddItem(source, item, amount, info, slot)
            return success
        elseif GetResourceState('qs-inventory') == 'started' then
            exports['qs-inventory']:AddItem(source, item, amount, slot, info)
            return true
        elseif GetResourceState('qb-inventory') == 'started' then
            exports['qb-inventory']:AddItem(source, item, amount or 1, slot or false, info, 'pc-multicharacter:GiveStarterItems')
            return true
        elseif GetResourceState('codem-inventory') == 'started' or GetResourceState('mInventory') == 'started' then
            exports['codem-inventory']:AddItem(source, item, amount, slot, info)
            return true
        elseif GetResourceState('core-inventory') == 'started' then
            exports['core-inventory']:addItem(source, item, amount, info)
            return true
        elseif GetResourceState('tgiann-inventory') == 'started' then
            exports['tgiann-inventory']:AddItem(source, item, amount, slot, info)
            return true
        elseif GetResourceState('origen_inventory') == 'started' then
            exports['origen_inventory']:AddItem(source, item, amount, slot, info)
            return true
        else
            local Player = Bridge.GetPlayer(source)
            if Player then
                if Bridge.Framework == 'ESX' then
                    return Player.addInventoryItem(item, amount)
                elseif Bridge.Framework == 'QBCORE' then
                    if Player.Functions and Player.Functions.AddItem then
                        return Player.Functions.AddItem(item, amount, slot or false, info)
                    end
                end
            end
        end
        return false
    end
```

**Adding Custom Inventory System**

1. **Add detection** in **server/main.lua** (after line 63):

```lua
elseif GetResourceState('your-inventory') == 'started' then
    exports['your-inventory']:GiveItem(src, v.item, v.amount or 1, info)
```

2. **Configure starter items**:
   * For QBCore: Modify `QBCore.Shared.StarterItems` in qb-core
   * For ESX: Modify **config.lua** (lines 44-48):

```lua
Config.ESX.StarterItems = {
    {name = 'phone', count = 1},
    {name = 'id_card', count = 1},
    {name = 'driver_license', count = 1},
    {name = 'water', count = 5},
    {name = 'burger', count = 5}
}
```
