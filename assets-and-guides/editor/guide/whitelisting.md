# Whitelisting & Permissions

## Access Control Overview

PC Crafting has three layers of access control that can be used independently or together:

1. **Global Player Whitelist:** Specific players always have access, regardless of job
2. **Job Whitelisting:** Tables restrict access to players with specific jobs and grades
3. **Admin Whitelist:** Specific players have admin panel access

![Access Control](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/Whitelisting/1.png)

## Global Player Whitelist

Configure in `config.lua`:

- `Config.Whitelisted = true/false` — Enable/disable the global whitelist gate
- `Config.WhitelistedPlayers` — Table of license identifiers that bypass all restrictions

Example entry in `Config.WhitelistedPlayers`:

```lua
["license:abc123..."] = true
```

When `Config.Whitelisted = true`, only players in this list can access any crafting table. If `false`, the list is ignored and tables use job-based restrictions only.

## Job Whitelisting

Job whitelisting restricts individual tables to players with specific jobs and grades. Configure per-table in `craftinglocations.lua`:

- `police = { grades = {2, 3, 4, 5} }` — Police officers grade 2 and above
- `ballas = { grades = {3, 4, 5} }` — Ballas gang members grade 3 and above
- `jobs = {}` — Empty jobs table = public access (anyone can use)

Enable job whitelisting globally with `Config.JobWhitelisting = true`. If disabled, all tables are publicly accessible.

Players not meeting the job requirement receive: *"None of your jobs are authorized to use this crafting table"* or *"Your rank is not high enough"*.

## Admin Whitelist

Admin access is controlled by `Config.WhitelistedAdmins` in `config.lua`. Admins can open the Admin Panel from within the crafting UI. Add identifiers in the format used by your framework:

- **QBX / QB (license2):** `"license2:abc123..."`
- **ESX (char):** `"char2:abc123..."`
- **QBCore (license):** `"license:abc123..."`

You can also manage the player whitelist from the Admin Panel → Access section without editing files directly.

## Access Denial Notifications

When a player is denied access, they receive one of these notifications:

- *"You are not authorized."* — Player not in global whitelist
- *"Invalid crafting table."* — Table not found or misconfigured
- *"Your rank is not high enough to use this crafting table."* — Job grade insufficient
- *"None of your jobs are authorized to use this crafting table."* — Wrong job entirely
