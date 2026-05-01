# Spawn

PC-Multicharacter detects and integrates with various spawn systems automatically.

**Supported Spawn Systems**

1. **qb-spawn** (default QBCore)
2. **qbx\_spawn** (Qbox variant)
3. **um-spawn**
4. **renzu\_spawn**
5. **Custom ESX spawn resources**

**Configuration Locations**

**bridge.lua (server-side, lines 294-313):**

```lua
local function setupSpawnEvents()
    if GetResourceState('qbx_spawn') == 'started' then
        Bridge.SpawnEvents.setupSpawns = 'qb-spawn:client:setupSpawns'
        Bridge.SpawnEvents.openUI = 'qb-spawn:client:openUI'
        Bridge.SpawnEvents.type = 'qbx_spawn'
    elseif GetResourceState('qb-spawn') == 'started' then
        Bridge.SpawnEvents.setupSpawns = 'qb-spawn:client:setupSpawns'
        Bridge.SpawnEvents.openUI = 'qb-spawn:client:openUI'
        Bridge.SpawnEvents.type = 'qb_spawn'
    elseif GetResourceState('um-spawn') == 'started' then
        Bridge.SpawnEvents.type = 'um_spawn'
    elseif GetResourceState('renzu_spawn') == 'started' then
        Bridge.SpawnEvents.type = 'renzu_spawn'
    else
        -- Default spawn events
        Bridge.SpawnEvents.setupSpawns = 'qb-spawn:client:setupSpawns'
        Bridge.SpawnEvents.openUI = 'qb-spawn:client:openUI'
        Bridge.SpawnEvents.type = 'default'
    end
end
```

**Adding Custom Spawn System**

1. **For QBCore**, add detection in **bridge.lua** (after line 305):

```lua
elseif GetResourceState('your-spawn') == 'started' then
    Bridge.SpawnEvents.type = 'your_spawn'
    Bridge.SpawnEvents.setupSpawns = 'your-spawn:client:setup'
    Bridge.SpawnEvents.openUI = 'your-spawn:client:open'
```

2. **For ESX**, configure in **config.lua** (lines 59-66):

```lua
Config.ESX.SpawnResource = 'your-spawn-resource'
Config.ESX.SpawnEvents = {
    setupSpawns = 'your-spawn:client:setupSpawns',
    openUI = 'your-spawn:client:openUI',
}
```

3. **Handle spawn in server/main.lua** (lines 205-216):

```lua
-- Add new spawn type handling
elseif Bridge.SpawnEvents.type == 'your_spawn' then
    TriggerClientEvent('your-spawn:client:showUI', src, cData)
```
