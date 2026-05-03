# Admin Panel — Overview & Pages

## Opening the Admin Panel

Use this command in-game:

```
/pcadmin
```

> **Note:** You must have the required permission/ace to use this command.

## What is the Admin Panel?

In-game configuration UI for managing pc-mechanic and pc-crafting-v2 without editing config files directly. Changes apply to live server memory instantly and can be exported to persist between restarts.

- **Mechanic panel** — configure shops, jobs, pricing, tuning, servicing, inspection, integrations, and more.
- **Crafting panel** — manage recipes, tables, whitelist, weapon attachments, parts, and models.
- **AI assistant** — ask questions about your config and get guided step-by-step walkthroughs.
- **Change history** — every modification is recorded as a session; restore any past state at any time.

![Admin Panel Overview](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/AdminGuide/images/Overview/1.png)

## Panel Layout

The panel is 1100×680px and scales to your viewport. Layout:

- **Left sidebar** — icon-based navigation with all available pages for the active panel. Scrollable if there are many pages.
- **Header row 1** — Mechanic / Crafting toggle, AI search bar (Ctrl+K), theme toggle, and close button.
- **Header row 2** — current page name, save status indicator, and session change tracker badge.
- **Main content area** — the active page's settings, scrollable.

![Admin Panel Layout](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/AdminGuide/images/Overview/2.png)

## Mechanic Pages

Pages available when the Mechanic panel is active:

- **General** — core settings and preferences for the resource.
- **Business & Jobs** — job system, employee roles, and business management.
- **Roles & Permissions** — configure role hierarchy and per-role permission sets.
- **Vehicle Systems** — mileage tracking, nitrous system, and repair kits.
- **Tuning** — performance upgrade options and tuning configuration.
- **Damage & Degradation** — damage-based part wear and degradation rates.
- **Servicing** — part durability and service interval settings.
- **Inspection** — inspection minigames, tools, and pass/fail thresholds.
- **Shop Locations** — define and manage mechanic shop zones.
- **Parts Shop** — online shop inventory and order settings.
- **Pricing** — dynamic pricing rules and economy settings.
- **Gameplay** — minigames, stance system, and player interactions.
- **Integrations** — framework bridges, UI libraries, and Discord webhooks.
- **Change History** — browse and restore past configuration sessions.
- **Export Configs** — download config files to persist changes after restart.

![Mechanic Pages Sidebar](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/AdminGuide/images/Overview/3.png)

## Crafting Pages

Switch to the Crafting panel for pc-crafting-v2 configuration:

- **Core Settings** — main crafting system toggles and global options.
- **Recipes** — items and weapons that can be crafted, with ingredients and amounts.
- **Tables** — crafting table locations, zones, and their settings.
- **Access Control** — player and admin whitelist management.
- **Weapon Attachments** — attachment unlock and crafting configurations.
- **Weapon Parts** — part damage frequencies and repair settings.
- **Weapon Models** — 3D model URL mappings for weapons.
- **Change History / Export** — same as mechanic panel; shared across both.

![Crafting Pages Sidebar](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/AdminGuide/images/Overview/4.png)
