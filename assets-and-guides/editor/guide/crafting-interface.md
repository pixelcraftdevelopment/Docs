# Crafting Interface

## Landing Page

When you open a crafting table, the landing page presents two main panels:

- **Weapons:** Lists all weapons available at this table that you can craft or repair. Each card shows the weapon image, name, and current serial/health if owned
- **Crafting (Items):** Lists all non-weapon items available at this table for crafting (e.g. handcuffs, lockpicks, etc.)

Use the **Search** bar at the top to filter items by name. Click any card to enter the detailed crafting/repair view for that item.

![Landing Page](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/CraftingInterface/1.png)

## Interface Tabs

Once you select a weapon or item, the detailed view has four tabs:

- **Mods:** View and apply weapon attachments (scopes, suppressors, grips, clips, tints, stocks, flashlights)
- **Table:** The crafting/repair workspace. Shows the 3D model on the left and the parts panel on the right. Drag parts from inventory or click to add/remove from the table
- **History:** Log of all previous crafting and repair operations performed at this table session
- **Queue:** Shows items currently being crafted, their remaining time, and pending items in the queue

## Inventory vs Crafting Table

In the Table tab, your available parts are shown in two panels:

1. **Inventory:** Parts currently in your player inventory
2. **Crafting Table:** Parts you have placed on the table from your inventory. Only parts on the table are used for crafting and repair

Transfer parts between inventory and table by clicking the part cards. Parts display their **Qty** (quantity) on the card. Parts with a health bar show their current condition.

## 3D Viewer Controls

The 3D weapon model viewer allows real-time interaction with the weapon assembly:

- **Mouse Hold + Drag:** Rotate the weapon model
- **Scroll Wheel:** Zoom in and out
- **Escape:** Exit the 3D view
- **Parts count:** Shows how many parts are currently placed on the model

As you add parts, they visually appear on the 3D model. When all required parts are on the table, the **Craft** button becomes active.

## Quantity Selector

When crafting non-weapon items that have `QuantitySelectorEnabled = true` in the config, a quantity input appears before confirming the craft. Lets you craft multiple units in a single operation, as long as you have sufficient materials for the selected quantity.
