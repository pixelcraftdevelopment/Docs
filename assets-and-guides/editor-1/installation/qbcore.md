---
description: Installation process for qbcore servers
---

# QBCORE

* **Download the Resource:** Download the PC-Multcharacter resource files from your fivem keymaster.
* **Extract the Files:** Extract the contents of the downloaded archive to your FiveM server's resources folder.
* Add this to qb-core/server/player.lua at the end of the file :&#x20;
  *

      ```lua
      -- =======================
      -- SERVER SIDE
      -- =======================
      function QBCore.Player.GetPlayerCharacters(license)
          local characters = {}
          local result = MySQL.query.await([[
              SELECT 
                  citizenid,
                  cid,
                  charinfo,
                  job,
                  money,
                  position,
                  metadata,
                  gang
              FROM players 
              WHERE license = ? 
              ORDER BY cid
          ]], {license})
          if not result then 
              return characters 
          end
          local tempCharacters = {}
          for i = 1, #result do
              local char = result[i]
              local charinfo = json.decode(char.charinfo or '{}')
              local job = json.decode(char.job or '{}')
              local gang = json.decode(char.gang or '{}')
              local money = json.decode(char.money or '{}')
              local position = json.decode(char.position or '{}')
              local metadata = json.decode(char.metadata or '{}')
              local slot = char.cid
              if tempCharacters[slot] then
                  while tempCharacters[slot] do
                      slot = slot + 1
                  end
              end
              tempCharacters[slot] = {
                  slot = slot,
                  citizenid = char.citizenid,
                  firstname = charinfo.firstname,
                  lastname = charinfo.lastname,
                  dateofbirth = charinfo.birthdate,
                  sex = charinfo.gender == 0 and 'm' or 'f',
                  nationality = charinfo.nationality,
                  job = job.label,
                  jobData = job,
                  grade = job.grade and job.grade.name or 'Unknown',
                  bank = money.bank or 0,
                  money = money.cash or 0,
                  cash = money.cash or 0, 
                  position = position,
                  metadata = metadata,
                  gang = gang, 
                  charinfo = charinfo 
              }
          end
          local citizenIds = {}
          for _, char in pairs(tempCharacters) do
              table.insert(citizenIds, char.citizenid)
          end
          if #citizenIds > 0 then
              local skinQuery = string.format('SELECT citizenid, model, skin FROM playerskins WHERE citizenid IN (%s)', 
                  table.concat((function()
                      local placeholders = {}
                      for i = 1, #citizenIds do
                          placeholders[i] = '?'
                      end
                      return placeholders
                  end)(), ','))
              local skins = MySQL.query.await(skinQuery, citizenIds)
              if skins then
                  for i = 1, #skins do
                      for slot, char in pairs(tempCharacters) do
                          if char.citizenid == skins[i].citizenid then
                              char.skin = json.decode(skins[i].skin or '{}')
                              char.model = skins[i].model
                              break
                          end
                      end
                  end
              end
          end
          for slot, char in pairs(tempCharacters) do
              characters[#characters + 1] = char
          end
          table.sort(characters, function(a, b)
              return (a.slot or 0) < (b.slot or 0)
          end)
          return characters
      end

      -- Export the function
      exports('GetPlayerCharacters', QBCore.Player.GetPlayerCharacters)


      function QBCore.Player.GetPlayerCharacterPositions(license)
          local positions = {}
          local result = MySQL.query.await([[
              SELECT 
                  citizenid,
                  cid,
                  position
              FROM players 
              WHERE license = ? 
              ORDER BY cid
          ]], {license})
          
          if not result then 
              return positions 
          end
          
          for i = 1, #result do
              local char = result[i]
              if char.position then
                  local pos = json.decode(char.position)
                  if pos and pos.z and pos.z > -100 then -- Validate position
                      positions[#positions + 1] = {
                          slot = char.cid,
                          citizenid = char.citizenid,
                          position = pos
                      }
                  end
              end
          end
          
          return positions
      end

      -- Export the function
      exports('GetPlayerCharacterPositions', QBCore.Player.GetPlayerCharacterPositions)
      ```
* Add this to qb-core/server/events.lua after the other callbacks :&#x20;
  *

      ```lua
      -- =======================
      -- SERVER SIDE
      -- =======================
      QBCore.Functions.CreateCallback('QBCore:Server:GetPlayerCharacters', function(source, cb)
          local license = QBCore.Functions.GetIdentifier(source, 'license')
          if not license then
              cb({})
              return
          end
          local characters = QBCore.Player.GetPlayerCharacters(license)
          cb(characters)
      end)

      QBCore.Functions.CreateCallback('QBCore:Server:GetPlayerCharacterPositions', function(source, cb)
          local license = QBCore.Functions.GetIdentifier(source, 'license')
          if not license then
              cb({})
              return
          end
          local positions = QBCore.Player.GetPlayerCharacterPositions(license)
          cb(positions)
      end)

      ```
* Add this to qb-core/client/functions.lua at the end of the file :&#x20;
  *

      ```lua
      -- =======================
      -- CLIENT SIDE
      -- =======================
      function QBCore.Functions.GetPlayerCharacters(cb)
          QBCore.Functions.TriggerCallback('QBCore:Server:GetPlayerCharacters', function(characters)
              cb(characters)
          end)
      end

      function QBCore.Functions.GetPlayerCharacterPositions(cb)
          QBCore.Functions.TriggerCallback('QBCore:Server:GetPlayerCharacterPositions', function(positions)
              cb(positions)
          end)
      end
      ```
* Configure the settings in `config.lua` according to your server's needs(won't be needed in most cases)
