# Apartment

PC-Multicharacter supports various apartment/housing systems.

**Supported Apartment Systems**

1. **qb-apartments** (default QBCore)
2. **qbx\_properties** (Qbox variant)
3. **0r-apartment-v2**
4. **qs-apartments**
5. **Custom ESX property systems**

**Configuration Locations**

**bridge.lua (lines 316-334):**

```lua
Bridge.ApartmentSystem = {}
local function setupApartmentSystem()
    if GetResourceState('qb-apartments') == 'started' then
        Bridge.ApartmentSystem.type = 'qb_apartments'
        Bridge.ApartmentSystem.event = 'apartments:client:setupSpawnUI'
    elseif GetResourceState('qbx_properties') == 'started' then
        Bridge.ApartmentSystem.type = 'qbx_properties'
        Bridge.ApartmentSystem.event = 'apartments:client:setupSpawnUI'
    elseif GetResourceState('0r-apartment-v2') == 'started' then
        Bridge.ApartmentSystem.type = '0r_apartments'
        Bridge.ApartmentSystem.event = 'apartments:client:setupSpawnUI'
    elseif GetResourceState('qs-apartments') == 'started' then
        Bridge.ApartmentSystem.type = 'qs_apartments'
        Bridge.ApartmentSystem.isServerEvent = true
        Bridge.ApartmentSystem.event = 'apartments:server:CreateApartment'
    else
        Bridge.ApartmentSystem.type = 'none'
    end
end
```

**Adding Custom Apartment System**

1. **Add detection** in **bridge.lua** (after line 327):

```lua
elseif GetResourceState('your-apartments') == 'started' then
    Bridge.ApartmentSystem.type = 'your_apartments'
    Bridge.ApartmentSystem.event = 'your-apartments:client:setup'
    Bridge.ApartmentSystem.isServerEvent = false -- or true if server event
```

2. **Handle apartment creation** in **server/main.lua** (lines 421-425):

```lua
-- Add after line 422
elseif Bridge.ApartmentSystem.type == 'your_apartments' then
    if Bridge.ApartmentSystem.isServerEvent then
        TriggerEvent(Bridge.ApartmentSystem.event, src, apartmentData)
    else
        TriggerClientEvent(Bridge.ApartmentSystem.event, src, newData)
    end
```

3. **For ESX**, configure in **config.lua** (lines 69-75):

```lua
Config.ESX.ApartmentResource = 'your-apartment-resource'
Config.ESX.ApartmentEvents = {
    setupUI = 'your-apartments:setupUI',
    setHome = 'your-apartments:setHome',
    enterProperty = 'your-apartments:enterProperty',
}
```
