# Tablet & Interaction

Settings in `pc-mechanic/config/config.lua` that govern the tablet, in-game interaction prompts, and minor UI behavior.

## Tablet

```lua
Config.UseTabletCommand   = "tablet"
Config.LetAdminsUseTablets = false
Config.AllowedConnectionDistance = 4.0
Config.EnableBusyCheck    = true
Config.NotifyAllEmployees = true
```

| Field | Purpose |
|-------|---------|
| `UseTabletCommand` | Command name to open the tablet. Set `false` to disable the command |
| `LetAdminsUseTablets` | If true, server admins can open the tablet without being on a mechanic job |
| `AllowedConnectionDistance` | Max distance (m) for tablet ↔ vehicle pairing |
| `EnableBusyCheck` | If true, the system checks whether the target player is busy before sending invoices/hire offers — reduces UI overlap |
| `NotifyAllEmployees` | If true, new orders notify every employee. If false, only on-duty mechanics are pinged |

## Interaction Controls

```lua
Config.CustomiseVehicleKey       = 38              -- E
Config.CustomiseVehiclePrompt    = "[E] Customise vehicle"
Config.FreecamKey                = "Tab"
Config.AutoPositionPlayer        = false
Config.MinigameInteractionDistance = 4.0
Config.PlayGameSounds            = true
```

| Field | Purpose |
|-------|---------|
| `CustomiseVehicleKey` | GTA control number to open customization (default 38 = E). Used at self-service shops |
| `CustomiseVehiclePrompt` | Help text shown on the prompt |
| `FreecamKey` | Key to toggle freecam in mod menu (e.g. `"Tab"`, `"F5"`, `"CapsLock"`) |
| `AutoPositionPlayer` | If true, the player is auto-positioned during minigames (e.g. squarely on the dyno platform) |
| `MinigameInteractionDistance` | Distance (m) at which interaction prompts for minigames appear |
| `PlayGameSounds` | If false, all in-game sound effects from the resource are silenced |

## Business Toggles

```lua
Config.NearbySelfFlag    = true
Config.allowOwnOrders    = true
```

| Field | Purpose |
|-------|---------|
| `NearbySelfFlag` | Show a "self" flag on nearby mechanics when displaying the mechanic list (e.g. invoicing UI) |
| `allowOwnOrders` | Allow mechanics to place orders for their own vehicles |

## UI Plate

```lua
Config.DiffPlateWhileModding = "BiteMe"
```

The plate displayed on the vehicle while modifications are being installed. Useful so the work-in-progress car doesn't show in plate-driven systems (police lookups, garage retrieval, etc.). Reverts to the real plate when work completes.

## Brand Image

```lua
Config.GitHubImageHost = "https://raw.githubusercontent.com/pixelcraftdevelopment/MechanicImages/main"
```

Base URL for tuning catalogue images. Don't change unless you're hosting your own images.

## Interactions

### Tablet & Roles

The tablet's contents are filtered by the role permissions table (`Config.Roles[role].permissions`). Even if `UseTabletCommand` is enabled, what a player sees inside depends on:

- `canAccessTablet` (open at all)
- `canAccessManagement` (management page)
- Plus all the per-action permissions documented in [Roles & Permissions](roles.md)

`LetAdminsUseTablets = true` only grants access for the admin role; it doesn't bypass per-action permissions inside.

### Tablet & Connection Distance

`AllowedConnectionDistance` is enforced per pairing — you can be far from the tablet's holder but you must be within this distance of the **vehicle** you're pairing with. Walking away from the car while paired drops the pairing.

### Busy Check

When `EnableBusyCheck = true`, sending an invoice or hire offer to a target who's already in a menu (any menu, ox_lib or otherwise) defers your action. Some servers prefer to skip this and let the new menu interrupt — set to false in that case.
