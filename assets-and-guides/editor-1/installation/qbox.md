---
description: Installation process for QBOX servers
---

# QBOX

* **Download the Resource:** Download the PC-Multcharacter resource files from your fivem keymaster.
* **Extract the Files:** Extract the contents of the downloaded archive to your FiveM server's resources folder.
* Set this flag : useExternalCharacters to true in qbx\_core/config/client.lua
* Add this to qbx\_core/bridge/qb/server/functions.lua at the end of the file :&#x20;
  *

      ```lua
      -- =======================
      -- SERVER SIDE
      -- =======================
      lib.callback.register('QBCore:Server:GetPlayerCharacters', function(source)
          local license2 = GetPlayerIdentifierByType(source, 'license2')
          local license = GetPlayerIdentifierByType(source, 'license')
          if not license2 and not license then
              return {}
          end
          local storage = require 'server.storage.main'
          local characters = MySQL.query.await([[
              SELECT 
                  p.citizenid,
                  p.charinfo,
                  p.money,
                  p.job,
                  p.gang,
                  p.position,
                  p.metadata,
                  UNIX_TIMESTAMP(p.last_logged_out) AS lastLoggedOutUnix,
                  ps.model,
                  ps.skin,
                  ps.active
              FROM players p
              LEFT JOIN playerskins ps ON p.citizenid = ps.citizenid AND ps.active = 1
              WHERE p.license = ? OR p.license = ?
              ORDER BY JSON_EXTRACT(p.charinfo, '$.cid') ASC
          ]], {license, license2})
          local formattedCharacters = {}
          for i = 1, #characters do
              local char = characters[i]
              local charinfo = json.decode(char.charinfo)
              local money = json.decode(char.money)
              local job = char.job and json.decode(char.job)
              local gang = char.gang and json.decode(char.gang)
              local metadata = json.decode(char.metadata)
              formattedCharacters[i] = {
                  citizenid = char.citizenid,
                  cid = charinfo.cid,
                  slot = charinfo.cid, 
                  charinfo = charinfo,
                  firstname = charinfo.firstname,
                  lastname = charinfo.lastname,
                  dateofbirth = charinfo.birthdate,
                  sex = charinfo.gender == 0 and 'm' or 'f',
                  nationality = charinfo.nationality,
                  job = job and {
                      name = job.name or 'unemployed', 
                      label = job.label or 'unemployed',
                      grade = job.grade or {name = '', level = 0}
                  } or {
                      name = 'unemployed',
                      label = 'unemployed',
                      grade = {name = '', level = 0}
                  },
                  gang = gang,
                  money = money,
                  position = char.position and json.decode(char.position) or nil,
                  metadata = metadata,
                  lastLoggedOut = char.lastLoggedOutUnix,
                  skin = char.skin and json.decode(char.skin) or nil,
                  model = char.model
              }
          end
          return formattedCharacters
      end)

      exports('GetPlayerCharacters', function(license)
          local characters = MySQL.query.await([[
              SELECT 
                  p.citizenid,
                  p.charinfo,
                  p.money,
                  p.job,
                  p.gang,
                  p.position,
                  p.metadata,
                  UNIX_TIMESTAMP(p.last_logged_out) AS lastLoggedOutUnix,
                  ps.model,
                  ps.skin,
                  ps.active
              FROM players p
              LEFT JOIN playerskins ps ON p.citizenid = ps.citizenid AND ps.active = 1
              WHERE p.license = ?
              ORDER BY JSON_EXTRACT(p.charinfo, '$.cid') ASC
          ]], {license})
          local formattedCharacters = {}
          for i = 1, #characters do
              local char = characters[i]
              local charinfo = json.decode(char.charinfo)
              local money = json.decode(char.money)
              local job = char.job and json.decode(char.job)
              local gang = char.gang and json.decode(char.gang)
              local metadata = json.decode(char.metadata)
              formattedCharacters[i] = {
                  citizenid = char.citizenid,
                  cid = charinfo.cid,
                  slot = charinfo.cid,
                  charinfo = charinfo,
                  firstname = charinfo.firstname,
                  lastname = charinfo.lastname,
                  dateofbirth = charinfo.birthdate,
                  sex = charinfo.gender == 0 and 'm' or 'f',
                  nationality = charinfo.nationality,
                  job = job and {
                      name = job.name or 'unemployed', -- Add job name for scene/clothing selection
                      label = job.label or 'unemployed',
                      grade = job.grade or {name = '', level = 0}
                  } or {
                      name = 'unemployed',
                      label = 'unemployed',
                      grade = {name = '', level = 0}
                  },
                  gang = gang,
                  money = money,
                  position = char.position and json.decode(char.position) or nil,
                  metadata = metadata,
                  lastLoggedOut = char.lastLoggedOutUnix,
                  skin = char.skin and json.decode(char.skin) or nil,
                  model = char.model
              }
          end
          return formattedCharacters
      end)

      lib.callback.register('QBCore:Server:GetPlayerCharacterPositions', function(source)
          local license2 = GetPlayerIdentifierByType(source, 'license2')
          local license = GetPlayerIdentifierByType(source, 'license')
          if not license2 and not license then
              return {}
          end
          
          local positions = MySQL.query.await([[
              SELECT 
                  p.citizenid,
                  JSON_EXTRACT(p.charinfo, '$.cid') AS cid,
                  p.position
              FROM players p
              WHERE p.license = ? OR p.license = ?
              ORDER BY JSON_EXTRACT(p.charinfo, '$.cid') ASC
          ]], {license, license2})
          
          local formattedPositions = {}
          for i = 1, #positions do
              local char = positions[i]
              if char.position then
                  local pos = json.decode(char.position)
                  if pos and pos.z and pos.z > -100 then -- Validate position
                      formattedPositions[i] = {
                          slot = tonumber(char.cid) or i,
                          citizenid = char.citizenid,
                          position = pos
                      }
                  end
              end
          end
          
          return formattedPositions
      end)
      ```
* Configure the settings in `config.lua` according to your server's needs(won't be needed in most cases)
