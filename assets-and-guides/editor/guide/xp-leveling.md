# XP & Leveling System

## Experience System Overview

PC Crafting includes an optional XP and leveling system. When enabled (`Config.expEnabled = true`), players earn XP by crafting weapons, crafting items, and repairing weapon parts. XP gates access to higher-tier recipes — you must reach the required XP threshold before you can craft certain items.

To disable the XP system entirely, set `Config.expEnabled = false` in `config.lua`. All items become accessible regardless of XP.

![XP & Leveling System](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/CraftingGuide/images/XPLeveling/1.png)

## Level Thresholds

Levels are defined in `Config.Levels` as a table of XP thresholds. The default config has three levels:

- **Level 1:** 0 – 999 XP — Beginner. Access to basic items and entry-level weapons
- **Level 2:** 1,000 – 2,099 XP — Intermediate. Access to mid-tier weapons and items
- **Level 3:** 2,100 – 3,199 XP — Advanced. Access to most weapons and recipes
- **Level 4 (Max):** 3,200+ XP — Master. Full access to all items and weapons

Modify `Config.Levels = {1000, 2100, 3200}` to adjust the thresholds. Add more entries to create additional levels.

## Earning XP

XP is earned through:

- **Crafting a weapon or item:** Each recipe has a `rewardXP` value (e.g. Marksman Rifle = 44 XP, AP Pistol = 20 XP)
- **Repairing a weapon part:** Each part type awards XP when repaired (see `Config.PartExperience`). Higher-value parts like `gas_block` (30 XP) and `receiver_spring` (29 XP) give the most

## Part XP Reference Table

XP awarded per part repair (from `Config.PartExperience`):

| Part | XP |
|------|----|
| `gas_block` | 30 |
| `receiver_spring` | 29 |
| `recoil_spring` | 27 |
| `reloader` | 26 |
| `trigger` | 25 |
| `gas_piston` | 24 |
| `barrel` | 23 |
| `hammer` | 22 |
| `chamber` | 21 |
| `cleaning_rod` | 20 |
| `receiver` | 19 |
| `stock` | 18 |
| `handguard` | 17 |
| `slide` | 16 |
| `grip` / `upper_handguard` | 15 |
| `lower_handguard` | 14 |
| `shoulder_guard` / `rear_guard` | 13 |
| `magazine` / `sight_holder` | 12 |
| `rail` | 11 |
| `macro` / `grip_right` | 9 |
| `front_sight` / `grip_left` | 7–8 |
| `rear_sight` | 8 |
| `magazine_cap` | 6 |
