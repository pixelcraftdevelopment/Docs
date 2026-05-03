# Compatibility

## Supported Frameworks

PC Crafting auto-detects your server's framework. Set `Config.Core = 'auto'` (default) for automatic detection, or specify manually:

- **QBCore** — `Config.Core = 'qb-core'`
- **QBX (Qbox)** — Auto-detected as QBCore variant
- **ESX** — `Config.Core = 'ESX'`

Framework-specific bridge files are in `bridge/Client/client.lua` and `bridge/Server/server.lua`. These handle player data, job checks, and notifications per framework.

## Supported Inventory Systems

Set `Config.Inventory = 'auto'` for automatic detection, or specify:

- **qb-inventory** — `Config.Inventory = 'qb-inventory'`
- **ox_inventory** — `Config.Inventory = 'ox_inventory'`
- **qs-inventory** — `Config.Inventory = 'qs-inventory'`
- **tgiann-inventory** — `Config.Inventory = 'tgiann-inventory'`

Inventory-specific crafting recipes and attachments are in `DATA-INVSPECIFIC/data-[inventory]/`. Ensure you copy the correct files to `data/` for your inventory system, or the resource handles this automatically on startup.

The inventory image path can also be configured manually: `Config.InventoryImagePath = 'nui://ox_inventory/web/images/'`. Use `'auto'` for automatic detection.

## Target Systems

The interaction system is configurable via `Config.Target` and `Config.InteractionType`:

- **qb-target** — QBCore's target system
- **ox_target** — ox_target system
- **false** — Disable target system entirely

Set `Config.InteractionType`:

- `'target'` — Use target system only (look at table and select option)
- `'textui'` — Use text UI prompt only (proximity key press)
- `'both'` — Both target and text UI active simultaneously

## Text UI & Notifications

Supported text UI systems (auto-detected or set via `Config.TextUI`):

- `ox_lib`, `okokTextUI`, `lation_ui`, `ps-ui`, `cd_drawtextui`, `qb-core`

Supported notification systems (`Config.Notifications`):

- `ox_lib`, `okokNotify`, `lation_ui`, `ps-ui`, `nox_notify`, `qb-core`, `ESX`

## Progress Bar Systems

Progress bars show during crafting and repair operations. Supported (`Config.ProgressBar`):

- `lation_ui` — Lation UI progress bar
- `ox-bar` — ox_lib linear progress bar
- `ox-circle` — ox_lib circular progress bar
- `qb` — QBCore built-in progress bar

## PC Blueprints Integration

If you use the companion **pc-blueprints** resource for managing blueprint ownership and distribution, enable it with:

```lua
Config.ExternalBlueprintResource = true
```

When enabled, blueprint checks are handled by the pc-blueprints resource via exports. If not using pc-blueprints, leave this as `false` and the built-in blueprint item check is used instead.

## Required Dependencies

- **ox_lib** — Required. Used for shared functions, UI elements, and data handling
- **oxmysql / mysql-async** — Recommended for database persistence (history, queue, player XP)
- **Your framework** — QBCore / QBX / ESX
- **Your inventory** — One of the supported inventory systems listed above
