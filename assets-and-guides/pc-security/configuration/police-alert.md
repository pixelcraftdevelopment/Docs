# Police Alert

* **Config.PoliceAlert:** This string specifies the server event used to alert the police. Ensure it matches the event used by your police script.
  * ps-dispatch:server:notify: Used for the [ps-dispatch](https://www.google.com/url?sa=E\&q=https%3A%2F%2Fgithub.com%2FProject-Sloth%2Fps-dispatch) script.
  * police:server:policeAlert: Used for the qb-policejob script.
* Ps-dispatch settings Add this to cl\_events.lua of ps-dispatch:
  *   local function VIPAttack()     local currentPos = GetEntityCoords(PlayerPedId())     local locationInfo = getStreetandZone(currentPos)     local gender = GetPedGender()     TriggerServerEvent("dispatch:server:notify", {         dispatchcodename = "VIPattack", -- has to match the codes in sv\_dispatchcodes.lua so that it generates the right blip         dispatchCode = "10-78",         firstStreet = locationInfo,         gender = gender,         model = nil,         plate = nil,         priority = 1, -- priority         firstColor = nil,         automaticGunfire = false,         origin = {             x = currentPos.x,             y = currentPos.y,             z = currentPos.z         },         dispatchMessage = \_U('VIPattack'), -- message         job = { "police" } -- jobs that will get the alerts     }) end

      exports('VIPAttack', VIPAttack)
* Add this to end of locales.lua of ps-dispatch:
  * \['VIPattack'] = "VIP under attack",
* Add this to end of dispatchcodes.lua in the dispatchCodes array:
  * \["VIPattack"] =  {displayCode = '10-78', description ="VIP under attack", radius = 0, recipientList = {'police'}, blipSprite = 110, blipColour = 1, blipScale = 1.5, blipLength = 2, sound = "Lose\_1st", sound2 = "GTAO\_FM\_Events\_Soundset", offset = "false", blipflash = "false"},
