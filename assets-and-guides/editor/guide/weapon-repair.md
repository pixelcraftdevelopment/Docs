# Weapon Repair

## How Weapon Damage Works

Weapons accumulate damage over time based on usage. Each part has a `damageFrequency` value (defined in `WeaponParts.lua`) that controls how quickly that part degrades. Higher values = faster damage.

The global weapon damage multiplier (`Config.WeaponDamageMultiplier`) scales the base damage rate per weapon. Default is `0.15` for most weapons.

When you select a damaged weapon in the crafting interface, the **Table** tab shows each part and its current health percentage. Parts below 100% can be repaired.

![Weapon Damage System](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/WeaponRepair/1.png)

## Step-by-Step: Repairing a Weapon

1. Select the damaged weapon from the Weapons panel on the landing page
2. Navigate to the **Table** tab — see the weapon's current parts listed with health bars
3. Click **Repair Mode** to enter repair mode
4. In repair mode, click a damaged part to remove it from the weapon. It appears in the "Damaged Parts" list
5. Ensure you have a replacement part (same type, full health) in your inventory or on the table
6. Place the new part onto the table to replace the damaged one
7. Once all damaged parts are replaced, all parts must be reassembled on the table
8. Click **Repair** — a progress bar plays for the `repairDuration` configured for each part
9. On completion, the weapon returns to your inventory in full condition and you earn XP

![Weapon Repair Process](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/WeaponRepair/2.png)

## Repair XP & Part Experience

Each part type awards a different amount of XP when repaired. Configured in `Config.PartExperience`. Notable values:

- `gas_block` — 30 XP (highest)
- `receiver_spring` — 29 XP
- `recoil_spring` — 27 XP
- `trigger` — 25 XP
- `barrel` — 23 XP
- `magazine_cap` — 6 XP (lowest)

XP gained from repairs stacks with crafting XP and contributes to your level progression.

## Repair Notifications

During repair operations, these toasts may appear:

- **Repair Started:** Repair process has begun
- **Repair Complete:** Item successfully repaired
- **Part in Perfect Condition:** The part does not need repair
- **Missing Part:** The required part was not found on the table
- **Insufficient Experience:** Your XP level is too low to repair this item
- **Please Reassemble:** All parts must be back on the table before confirming repair
