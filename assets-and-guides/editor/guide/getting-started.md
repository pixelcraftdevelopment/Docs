# Getting Started with PC Crafting

## What is PC Crafting?

PC Crafting v2 is an advanced weapon crafting, repair, and item crafting resource for FiveM. Supports multiple frameworks (QBCore, ESX, QBX) and multiple inventory systems, with a fully 3D interactive interface for assembling, repairing, and customizing weapons.

**Key Features:**

- **3D Weapon Assembly:** Interactively place parts on a 3D model to craft weapons
- **Weapon Repair:** Disassemble damaged weapons, repair parts, and reassemble
- **Item Crafting:** Craft non-weapon items using configurable material recipes
- **Attachment System:** Apply scopes, suppressors, grips, clips, tints, and more
- **XP & Leveling:** Earn experience points through crafting and repair
- **Queue System:** Queue multiple items for sequential crafting
- **Placeable Tables:** Portable crafting tables players can place and pack up
- **Discord Logging:** Webhook-based logs for crafting, repair, economy, and table events

![PC Crafting Overview](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/GettingStarted/1.png)

## Accessing a Crafting Table

Two types of tables:

- **Static Tables:** Fixed at configured coordinates, accessible within a set radius
- **Placeable Tables:** Portable tables that authorized players can place and pack up

**To open a crafting table:**

1. Walk up to a crafting table within its interaction radius
2. If using **target** mode: look at the table and select "Use Crafting Table" from the target menu
3. If using **textui** mode: press `[E]` when the prompt appears
4. The crafting interface opens showing items and weapons available at this table
5. If job whitelisting is active, you must have the correct job and grade to access certain tables

## General Requirements

Before you can craft or repair weapons:

- **Blueprint (if required):** Some weapons require a blueprint item in your inventory. Blueprints are named `bp[weaponname]` (e.g. `bpassaultrifle`)
- **Weapon Parts:** Parts such as barrel, grip, trigger, stock, magazine, etc. must be in your inventory
- **Required XP:** If the XP system is enabled, you must meet the minimum XP threshold for that item
- **Job/Whitelist:** Some tables are restricted to specific jobs and grades

> **Tip:** Use `/giveitem [name] [amount]` to obtain any item for testing purposes.
