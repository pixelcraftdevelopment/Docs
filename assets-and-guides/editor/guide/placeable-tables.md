# Placeable Tables

## What are Placeable Tables?

Placeable tables are portable crafting benches players can carry as inventory items and deploy anywhere in the world. Unlike static tables fixed to set coordinates, placeable tables follow the player and can be set up on-demand.

Enable placeable tables by setting `Config.EnableTable = true` in `config.lua`. Three default table types are included:

- **crafting_table_basic:** Basic portable table (`prop_custom_bench_pc`). Available items: common weapons and tools (assault rifle, combat pistol, pistol, handcuffs, etc.)
- **crafting_table_advanced:** Advanced table (`gr_prop_gr_bench_03b`). MK2 weapons and high-tier attachments. Requires Ballas job grade 3+
- **crafting_table_police:** Police-grade table (`gr_prop_gr_bench_03b`). Police weapons, ammo, and equipment. Requires Police job grade 3+

![Placeable Crafting Table](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/PlaceableTables/1.png)

## Placing a Table

1. Obtain the table item in your inventory (e.g. `crafting_table_basic`)
2. Use the item from your inventory to enter table placement mode
3. A ghost preview of the table prop appears at your cursor — position it where you want the table
4. Use the placement controls to adjust:

**Placement Controls:**

- **WASD / Arrow Keys:** Move table horizontally
- **Q / E:** Move table up/down
- **Mouse wheel / R:** Rotate the table
- **F:** Snap to ground
- **Enter / Confirm:** Place the table
- **Backspace / Cancel:** Cancel placement
- **H:** Toggle controls help overlay
- **+/-:** Increase/decrease movement speed

5. Confirm placement — a placement animation plays (if enabled)
6. The table spawns in the world. Interact with it like a static table

## Packing Up a Table

1. Approach your placed table
2. Use the target (or press E) and select **"Pick Table"** from the menu
3. A confirmation dialog appears: *"Are you sure you want to pack up this crafting table?"*
4. Confirm — the pickup animation plays and the table returns to your inventory

> **Note:** Only the player who placed the table (or an admin) can pack it up.

## Placeable Table Configuration

Key options in `config.lua`:

- `Config.TableModel` — Default prop model for tables (`'gr_prop_gr_bench_03b'`)
- `Config.HeadingTable` — Default table heading angle (`180.0`)
- `Config.PlaceableAnimations.enableAnimation` — Play character animation when placing/picking up
- `Config.PlaceableAnimations.enableProgressBar` — Show progress bar during placement animation
- `Config.PlaceableAnimations.walkToLocation` — Character walks to table before placing
- `Config.PlaceableAnimations.place/pickup` — Configure animation dict, clip, label, and duration
