---
description: Installation process for ESX servers
---

# ESX

* **Download the Resource:** Download the PC-Multcharacter resource files from your fivem keymaster.
* **Extract the Files:** Extract the contents of the downloaded archive to your FiveM server's resources folder.
* Add this to es\_extended/server/functions.lua at the end of the file :&#x20;
  *

      ```lua
      -- =======================
      -- SERVER SIDE
      -- =======================
      function ESX.GetPlayerCharacters(license)
          local characters = {}
          local licenseHash = string.match(license, "license:(.+)") or license
          local searchPattern = '%:' .. licenseHash .. '%'
          local result = MySQL.query.await([[
              SELECT 
                  identifier,
                  firstname,
                  lastname,
                  dateofbirth,
                  sex,
                  height,
                  job,
                  job_grade,
                  accounts,
                  skin,
                  position,
                  metadata,
                  `group`,
                  phone_number
              FROM users 
              WHERE identifier LIKE ?
              ORDER BY identifier
          ]], {searchPattern})
          if not result then 
              return characters 
          end
          for i = 1, #result do
              local char = result[i]
              local charNum = tonumber(string.match(char.identifier, 'char(%d+):'))
              if charNum then
                  local accounts = json.decode(char.accounts or '{}')
                  local skin = json.decode(char.skin or '{}')
                  local position = json.decode(char.position or '{}')
                  local metadata = json.decode(char.metadata or '{}')
                  local jobLabel = char.job
                  if ESX.Jobs and ESX.Jobs[char.job] then
                      jobLabel = ESX.Jobs[char.job].label or char.job
                  end
                  characters[#characters + 1] = {
                      slot = charNum,
                      identifier = char.identifier,
                      citizenid = char.identifier, 
                      firstname = char.firstname or 'Unknown',
                      lastname = char.lastname or 'Player',
                      dateofbirth = char.dateofbirth or '1990-01-01',
                      sex = char.sex or 'm',
                      nationality = 'American',
                      height = char.height or 120,
                      job = {
                          name = char.job, tion
                          label = jobLabel,
                          grade = {
                              name = char.job_grade and tostring(char.job_grade) or '0',
                              level = char.job_grade or 0
                          }
                      },
                      money = {
                          cash = accounts.money or 0,
                          bank = accounts.bank or 0
                      },
                      skin = skin,
                      position = position,
                      metadata = metadata,
                      group = char.group or 'user',
                      charinfo = { 
                          firstname = char.firstname or 'Unknown',
                          lastname = char.lastname or 'Player',
                          birthdate = char.dateofbirth or '1990-01-01',
                          gender = char.sex == 'm' and 0 or 1,
                          nationality = 'American',
                          phone = char.phone_number or '000-000-0000'
                      }
                  }
              end
          end
          table.sort(characters, function(a, b)
              return (a.slot or 0) < (b.slot or 0)
          end)
          return characters
      end

      -- Export the function
      exports('GetPlayerCharacters', ESX.GetPlayerCharacters)

      function ESX.GetPlayerCharacterPositions(license)
          local positions = {}
          local licenseHash = string.match(license, "license:(.+)") or license
          local searchPattern = '%:' .. licenseHash .. '%'
          local result = MySQL.query.await([[
              SELECT 
                  identifier,
                  position
              FROM users 
              WHERE identifier LIKE ? 
              ORDER BY identifier
          ]], {searchPattern})
          
          if not result then 
              return positions 
          end
          
          for i = 1, #result do
              local char = result[i]
              local charNum = tonumber(string.match(char.identifier, 'char(%d+):'))
              if charNum and char.position then
                  local pos = json.decode(char.position)
                  if pos and pos.z and pos.z > -100 then -- Validate position
                      positions[#positions + 1] = {
                          slot = charNum,
                          identifier = char.identifier,
                          position = pos
                      }
                  end
              end
          end
          
          return positions
      end

      -- Export the function
      exports('GetPlayerCharacterPositions', ESX.GetPlayerCharacterPositions)
      ```
* Add this to es\_extended/server/modules/callback.lua after the other callbacks :&#x20;
  *

      ```lua
      -- =======================
      -- SERVER SIDE
      -- =======================
      ESX.RegisterServerCallback('ESX:GetPlayerCharacters', function(source, cb)
          if not ESX.GetIdentifier then
              cb({})
              return
          end
          local identifier = ESX.GetIdentifier(source)
          if not identifier then
              cb({})
              return
          end
          if not string.match(identifier, "^license:") then
              identifier = "license:" .. identifier
          end
          local characters = ESX.GetPlayerCharacters(identifier)
          cb(characters)
      end)

      ESX.RegisterServerCallback('ESX:GetPlayerCharacterPositions', function(source, cb)
          if not ESX.GetIdentifier then
              cb({})
              return
          end
          local identifier = ESX.GetIdentifier(source)
          if not identifier then
              cb({})
              return
          end
          if not string.match(identifier, "^license:") then
              identifier = "license:" .. identifier
          end
          local positions = ESX.GetPlayerCharacterPositions(identifier)
          cb(positions)
      end)

      ```
* Add this to es\_extended/client/functions at the end of the file :&#x20;
  *

      ```lua
      -- =======================
      -- CLIENT SIDE
      -- =======================
      function ESX.GetPlayerCharacters(cb)
          ESX.TriggerServerCallback('ESX:GetPlayerCharacters', function(characters)
              cb(characters)
          end)
      end
      function ESX.GetPlayerCharacterPositions(cb)
          ESX.TriggerServerCallback('ESX:GetPlayerCharacterPositions', function(positions)
              cb(positions)
          end)
      end

      ```
* Configure the settings in `config.lua` according to your server's needs(won't be needed in most cases)
