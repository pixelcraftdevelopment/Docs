# Item Crafting

## Non-Weapon Item Crafting

Beyond weapons, the crafting system supports regular inventory items such as handcuffs, lockpicks, repair kits, drill tools, and any custom item your server defines. These appear in the **Crafting** panel on the landing page.

Item recipes are defined in `craftingRecipes.lua` and can include a 3D prop model preview, blueprint requirement, repair functionality, and configurable material lists.

![Item Crafting Interface](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/ItemCrafting/1.png)

## Item Recipe Structure

Each item entry in `craftingRecipes.lua` supports:

- `name` — Item name (must match inventory item name)
- `label` — Display name shown in the UI
- `blueprint` — Whether a blueprint is required (`true`/`false`)
- `threeD` — Whether to show a 3D prop model preview
- `model` — Prop model name for 3D preview (e.g. `'prop_cs_cuffs_01'`)
- `description` — Short item description
- `requiredXp` — Minimum XP to craft
- `rewardXP` — XP earned on success
- `craftDuration` — Crafting time in milliseconds
- `repairDuration` — Repair time (if item is also repairable)
- `requiredMaterials` — Array of `{name, label, image, amount}` material objects
- `requiredRepairMaterials` — Array of materials for repair (if applicable)

## Step-by-Step: Crafting an Item

1. Obtain all required material items in your inventory (e.g. `steel`, `metalscrap`, `aluminum`)
2. Open a crafting table that has the target item in its `whitelistedItems`
3. Click the item card in the **Crafting** panel
4. Review the required materials panel — it shows what you need and how much you have
5. Transfer materials from your inventory to the crafting table
6. If quantity selection is enabled, choose how many you wish to craft
7. Click **Craft** — the progress bar plays for `craftDuration`
8. On success, the item(s) appear in your inventory and you earn the configured `rewardXP`

## Example Items

Some example items included in the default recipes:

- **Handcuffs** — Requires: 24x steel, 36x metalscrap, 28x aluminum. XP: 10 req / 6 reward. Duration: 2 min
- **Lockpick** — Custom materials defined in your craftingRecipes.lua
- **Repair Kit** — Tool for vehicle/weapon repairs
- **Electronic Kit** — Electronics components
- **Gate Crack Tool** — Used for criminal activities

> **Note:** All item recipes are fully customizable in `data/craftingRecipes.lua` or your pack's recipes file. Add any item supported by your inventory system.
