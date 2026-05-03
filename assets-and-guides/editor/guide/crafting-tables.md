# Crafting Tables

## Static Crafting Tables

Static tables are fixed at specific in-world coordinates. Defined in `data/craftinglocations.lua` (or your pack's `craftinglocations.lua`). Each entry supports:

- `name` — Display name for the table
- `coordinates` — `{x, y, z, heading, radius}` — World position and interaction radius
- `blip` — Map blip configuration (`enabled`, `sprite`, `color`, `scale`, `label`)
- `spawnTable` — If `true`, spawns a physical prop model at this location
- `whitelistedItems` — Array of item/weapon names accessible at this table
- `jobs` — Job whitelist: `{ jobname = { grades = {2, 3, 4} } }`. Leave empty `{}` for public access

![Crafting Table Setup](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/CraftingTables/1.png)

## Default Table Locations (Vanilla Pack)

The vanilla pack includes the following preconfigured tables:

- **Police Station** — `x: -3.31, y: -1821.18, z: 29.74` — Jobs: police (gr. 2–5), ambulance (gr. 3–5)
- **Gun Store** — `x: 60.24, y: -346.59, z: 41.80` — Jobs: police, ambulance
- **Red Garage 1** — `x: -295.60, y: -767.31, z: 52.25` — Jobs: ballas (gr. 2–5), police (gr. 2–3)
- **Humane Labs** — `x: 3555.01, y: 3669.26, z: 27.12` — Police only, limited item list
- **Hanger** — `x: -1877.63, y: 2965.62, z: 31.81` — Police only, weapons and attachments
- **Red Garages 2–4** — Various restricted access, limited item lists

## Shared Table Inventories

When `Config.SharedStashes = true`, all players using the same table share a single inventory pool. Parts placed on the table by one player are visible to others at the same table.

Set `SharedStashes = false` to give each player their own private table inventory that persists between sessions.

## Adding New Tables

To add a new static table, append a new entry to `craftingLocations` in `data/craftinglocations.lua`. Copy an existing entry and modify:

1. Set a unique `name`
2. Update `coordinates` with the in-game position (use `/coords` to get your current position)
3. Set `spawnTable = true` if you want the bench prop to spawn there
4. Populate `whitelistedItems` with all item/weapon names available at this table
5. Configure `jobs` for job whitelisting, or leave empty for public access
6. Optionally enable a `blip` to show the table on the minimap

> **Tip:** Restart the resource after adding or modifying table entries for changes to take effect.
