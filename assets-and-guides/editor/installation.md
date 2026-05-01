# Installation

* **Download the Resource:** Download the PC-crafting-v2 resource files from your fivem keymaster.
* **Extract the Files:** Extract the contents of the downloaded archive to your FiveM server's resources folder.
* Place in the resources folder and run. If you face any problem, continue on with the steps below and fresh installation.
* **Upload database**: Run the given sql files in your server's database.
* **Items** : Add the given items in the v2 items file to your server's items folder(qb-core/shared/items.lua for qbcore and data/items.lua for ox-inventory)
* **Images**:  Add Items images to the images folder of your inventory.
* Transfer the related data files from data-esx-qbox or data-qb folder into data folder according to your framework
* If you use **qb-weapons** specifically, add this code to the main.lua file on client side :&#x20;

```lua
exports('getCurrentWeapon', function()
    if not LocalPlayer.state.isLoggedIn then
        return nil
    end
    if not CurrentWeaponData then
        return 'weapon_unarmed'
    end
    return CurrentWeaponData
end)
```

* **Add to Server.cfg:** Add the following line to your server's server.cfg file to ensure the resource starts automatically.

```
start pc-crafting-v2
```
