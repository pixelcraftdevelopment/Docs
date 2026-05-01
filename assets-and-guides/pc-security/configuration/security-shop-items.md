# Security Shop Items

This table defines items available for purchase in the security shop. Players can spend their earned experience points to acquire these items.

```
Config.SecurityShopItems = {
    ["advancedrepairkit"] = { --Spawncode
        name = "Advanced Repair Kit",
        description = "A high-quality kit for vehicle repairs.",
        spawncode="advancedrepairkit", --Spawncode from items.lua
        price = "4 Exp", --Price of item
        stock_amount = 5, --Stock amount that resets before script restart
        max_buy = 2, --Max amount that can be bought at once
        requiredLevel = 1, -- Required level to buy this item
        imageUrl = "advancedkit.png" --Image from qb-inventory/html/images
    },
    ---You can add more shop items with the same format(Item images need to be added to main script folder security/html/build)
}
```

content\_copyUse code [with caution](https://support.google.com/legal/answer/13505487).Lua

* **\[spawncode]:** Each item is identified by its unique spawncode, acting as the key in the table.
  * **name:** The display name of the item.
  * **description:** A brief description of the item.
  * **spawncode:** The item's spawncode, used for inventory management.
  * **price:** The price of the item in experience points.
  * **stock\_amount:** The initial stock of the item in the shop. This value resets on server restart.
  * **max\_buy:** The maximum quantity of this item a player can purchase at once.
  * **requiredLevel:** The minimum player level required to purchase this item.
  * **imageUrl:** The file name (without extension) of the item's image, located in the security/html/build/images directory.
