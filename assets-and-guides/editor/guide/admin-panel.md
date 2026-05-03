# Admin Panel

## Opening the Admin Panel

The Admin Panel is an in-game management interface for server admins. Access it via the crafting UI when logged in as a whitelisted admin. Admins are defined in `Config.WhitelistedAdmins` in `config.lua`.

The admin panel has five main sections accessible via the sidebar:

- **Core** — Global resource settings
- **Weapons** — Manage craftable weapon configurations
- **Items** — Manage craftable item configurations
- **Tables** — Manage static and placeable crafting table definitions
- **Access** — Manage the global player whitelist

## Core Settings

Manages the main resource toggles:

- **Language:** Switch the active locale language
- **Enable Table:** Toggle whether crafting tables are active
- **Enable PC Logs:** Toggle Discord webhook logging
- **Job Whitelisting:** Toggle whether jobs are required for table access
- **Enable Usable Tables:** Toggle placeable table functionality
- **Experience Enabled:** Toggle the XP/leveling system

Changes save immediately on **Save Settings**. The "Unsaved changes" indicator shows when there are pending changes.

## Weapons Management

Add, edit, and remove craftable weapon configurations:

- **Add Weapon:** Create a new weapon recipe entry. Enter the weapon name (must start with `weapon_`)
- **Base Damage:** Set the weapon's base damage percentage for wear calculations
- **Experience:** Set required XP and reward XP for this weapon
- **Blueprint:** Toggle blueprint requirement on/off
- **Image:** Set the inventory image filename
- **3D Model:** Toggle 3D viewer for this weapon
- **Parts:** Add/remove weapon parts and set their damage frequency
- **Template:** Load a template set of parts for a weapon category

## Items Management

Add and configure non-weapon item recipes:

- **Add Item:** Create a new item recipe. Enter the inventory item name
- **Label / Description / Heading:** Set display information
- **Required / Reward XP:** Configure experience requirements and rewards
- **Craft Duration / Repair Duration:** Set time for crafting and repair in ms
- **Model / 3D:** Set a prop model name and toggle 3D preview
- **Blueprint:** Toggle blueprint requirement
- **Required Items:** Add materials with item name and quantity
- **Proximity:** Set interaction proximity for the prop

> **Note:** Set `Model` field before enabling 3D (`templatewarning: "Uncheck 3d box first"`)

## Tables Management

Manage both static tables and placeable table definitions:

**Static Tables:**

- Add new table — set name, coordinates (x, y, z, heading, radius)
- Configure whitelisted jobs and their allowed grades
- Select available items from the full item/weapon list (Select All option available)
- Set a custom heading rotation for the spawned table prop

**Usable (Placeable) Tables:**

- Define placeable table types by name (e.g. `crafting_table_basic`)
- Each type has its own item whitelist and optional job restrictions

## Access (Global Whitelist)

Manage the global player whitelist by license, server ID, or player name. Whitelisted players can access all tables regardless of job whitelisting settings.

- **FiveM License:** Enter the player's FiveM license identifier
- **Server ID:** Enter the player's current server ID for quick addition
- **Player Name:** Search by name (if online)
