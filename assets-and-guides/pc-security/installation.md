# Installation

* **Download the Resource:** Download the PC-Security resource files from your fivem keymaster.
* **Extract the Files:** Extract the contents of the downloaded archive to your FiveM server's resources folder.
* **Add to Server.cfg:** Add the following line to your server's server.cfg file to ensure the resource starts automatically:

```
start PC-Security
```

* Put these 2 lines in your items.lua file in \[qb]/qb-core/shared folder-
  * &#x20;\['s\_tablet2']                       = {\['name'] = 's\_tablet2',                         \['label'] = 'Secret Tablet',             \['weight'] = 2000,         \['type'] = 'item',         \['image'] = 'oppose\_tablet.png',           \['unique'] = false,         \['useable'] = true,     \['shouldClose'] = true,      \['combinable'] = nil,   \['description'] = 'Secret tablet'},&#x20;
  * \['s\_tablet1']                       = {\['name'] = 's\_tablet1',                         \['label'] = 'Contractor Tablet',         \['weight'] = 2000,         \['type'] = 'item',         \['image'] = 'contractor\_tablet.png',       \['unique'] = false,         \['useable'] = true,     \['shouldClose'] = true,      \['combinable'] = nil,   \['description'] = 'Contractor tablet'},
  * For ESX, run this query in your Database:
    * INSERT INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`) VALUES ('s\_tablet1', 'Security Tablet', 1, 0, 1), ('s\_tablet2', 'Secret Tablet', 1, 0, 1);
  * Put the images of the 2 tablets named contractor\_tablet and oppose\_tablet in qb-inventory/html/images.
