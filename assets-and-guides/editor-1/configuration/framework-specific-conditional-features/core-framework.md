# Core Framework

• **Garage System** - QBCore only

```lua
-- server/main.lua:74-77
if Bridge.Framework ~= 'QBCORE' then
    return -- Garages not loaded for ESX
end
```

• **Routing Buckets** - ESX only

```lua
-- server/main.lua:172-174
if Bridge.Framework == 'ESX' then
    local routingBucket = math.random(99, 999)
    SetPlayerRoutingBucket(src, routingBucket)
end
```

• **Starter Items Handling**

```lua
-- ESX: Direct inventory addition
Player.addInventoryItem(itemName, itemCount)

-- QBCore: Metadata support for ID cards
if v.item == "id_card" then
    info.citizenid = Player.PlayerData.citizenid
    -- Additional metadata...
end
```
