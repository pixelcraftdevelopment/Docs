# Attachments

## Attachment System Overview

The Mods tab lets players equip weapon attachments to owned weapons. Attachments modify behavior, aesthetics, or both. Organized by category, each requires a specific attachment item in your inventory.

Each category shows the currently equipped attachment (if any) along with all available options for that weapon. Only attachments compatible with the specific weapon model are shown.

![Attachment System](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/Attachments/1.png)

## Attachment Categories

- **Scopes:** Long-range optics for precision shooting. Items: `at_scope_small`, `at_scope_medium`, `at_scope_large`, `at_scope_advanced`, `at_scope_holo`, `at_scope_macro`, `at_scope_nv`, `at_scope_thermal`
- **Suppressors:** Reduces muzzle sound and flash. Items: `at_suppressor_light`, `at_suppressor_heavy`, plus weapon-specific variants like `pistol_suppressor`, `smg_suppressor`, `rifle_suppressor`
- **Grips:** Improves handling and reduces recoil. Items: `at_grip`, `grip_attachment`, plus weapon-class variants (`rifle_grip`, `smg_grip`, etc.)
- **Flashlights:** Underbarrel torch for low-light situations. Items: `at_flashlight`, `flashlight_attachment`, plus class variants
- **Clips (Extended Magazines):** Increases magazine capacity. Items: `at_clip_extended_pistol`, `at_clip_extended_smg`, `at_clip_drum_smg`, and class variants like `rifle_extendedclip`, `rifle_drum`
- **Tints:** Cosmetic weapon skin / finish. Item: `at_skin_luxe`
- **Stocks:** Adjustable buttstocks. Items: `at_barrel`, `barrel_attachment`, class variants like `smg_barrel`, `sniper_barrel`, `rifle_barrel`

## Applying Attachments

1. Open the crafting table and select the weapon you want to mod
2. Navigate to the **Mods** tab
3. Browse attachment categories — each shows a description and the required item
4. Click an attachment to equip it. The attachment item is consumed from your inventory
5. The weapon updates immediately. The previously equipped attachment (if any) is returned to your inventory
6. Click "None" to remove an attachment without equipping a new one

> **Note:** The number of attachment slots shown depends on the weapon type. Not all categories are available for every weapon.

![Attachment Mods Tab](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/Attachments/2.png)

## Configuring Attachments

Supported attachments per weapon are defined in `data/attachments.lua` (or pack-specific `attachments.lua`). Each entry maps a weapon name to a list of attachment items it accepts per category. Server owners can add or remove attachment items per weapon in this file.

Inventory-specific attachment definitions (for QB, QS, ESX+OX) are in `DATA-INVSPECIFIC/data-[framework]/attachments.lua` — use the correct file for your inventory system.
