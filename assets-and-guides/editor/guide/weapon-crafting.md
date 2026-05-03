# Weapon Crafting

## Crafting Overview

Weapon crafting lets players assemble weapons from individual parts using the 3D interactive table. Each weapon has a defined set of required parts (e.g. barrel, grip, trigger, stock, magazine) that must all be placed on the table before crafting can begin.

Each craftable weapon defined in `craftingRecipes.lua` has the following properties:

- **blueprint:** Whether a blueprint item is required in your inventory
- **threeD:** Whether the 3D model viewer is shown during crafting
- **requiredXp:** Minimum XP needed to craft this weapon
- **rewardXP:** XP gained upon successful craft
- **craftDuration:** Time in milliseconds the crafting process takes (e.g. 120000 = 2 minutes)
- **requiredMaterials:** List of part items and quantities needed

![Weapon Crafting Overview](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/WeaponCrafting/1.png)

## Step-by-Step: Crafting a Weapon

1. Obtain the required weapon parts (e.g. `barrel`, `grip`, `trigger`) and optionally a blueprint (`bpassaultrifle`) in your inventory
2. Approach a crafting table that has the desired weapon in its `whitelistedItems` list
3. Open the table and select the weapon card from the Weapons landing panel
4. Navigate to the **Table** tab
5. Click each required part in your inventory panel to transfer it to the crafting table
6. The 3D model updates as you place parts — watch the **Parts Available** counter increase
7. Once all required parts are on the table, click **Craft**
8. A progress bar plays for the configured `craftDuration` time
9. On completion you receive the crafted weapon in your inventory and earn the `rewardXP`

![Weapon Crafting Process](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/WeaponCrafting/2.png)

## Blueprints

When a weapon recipe has `blueprint = true`, the player must hold a blueprint item in their inventory before crafting. Blueprint items follow the naming convention `bp[weaponname]`:

- `bpassaultrifle` → Assault Rifle blueprint
- `bppistol` → Pistol blueprint
- `bpsmg` → SMG blueprint

By default (`Config.blueprintConsumed = false`), the blueprint is **not consumed** on use. Set `blueprintConsumed = true` in `config.lua` to consume it. If using the `pc-blueprints` resource, set `Config.ExternalBlueprintResource = true` for automatic detection.

## Common Weapon Parts

Each weapon uses a subset of the following parts (defined per weapon in `WeaponParts.lua`):

- `barrel` — Main barrel component. High damage frequency (0.85)
- `grip` — Pistol grip. Moderate damage frequency (0.40)
- `trigger` — Firing mechanism. Highest damage frequency (1.05+)
- `stock` — Buttstock for rifles/SMGs (0.30)
- `magazine` — Ammunition feeding device (0.40)
- `handguard` — Fore-end guard (0.50)
- `front_sight` / `rear_sight` — Iron sights (0.50–0.60)
- `hammer` / `slide` / `recoil_spring` — Pistol internals
- `rail` / `reloader` — MK2 weapon components
- `gas_block` / `gas_piston` / `lower_handguard` — Rifle internals
