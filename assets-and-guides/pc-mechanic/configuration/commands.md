# Commands

```lua
Config.RepairCommand          = "fix"
Config.SetOwnerCommand        = "setowner"
Config.UseTabletCommand       = "tablet"
Config.ViewRepairZonesCommand = "viewzones"
```

| Field | Default | Purpose | Permission |
|-------|---------|---------|-----------|
| `RepairCommand` | `fix` | Admin command to fully repair the targeted vehicle | Server admin |
| `SetOwnerCommand` | `setowner` | Set an owned shop's owner | Server admin |
| `UseTabletCommand` | `tablet` | Open the mechanic tablet | Mechanic on duty (or admin if `LetAdminsUseTablets = true`) |
| `ViewRepairZonesCommand` | `viewzones` | Visualize all repair zones at the nearest shop | Server admin |

Set any of these to `false` (or empty string) to disable that command.

## Notes

### `RepairCommand`

Hard-resets a vehicle to 100% body and engine health. Bypasses the wear system entirely — the next inspection will show 100% on every part. Don't use as a normal repair flow; reserve for admin fixups.

### `SetOwnerCommand`

After installing PC-Mechanic, owned shops have no assigned owner. Use this command to set an initial owner:

```
/setowner <shopId> <playerId>
```

Once set, the owner can hire other employees through the tablet's staff management. Until set, the shop functions but has no management chain.

### `UseTabletCommand`

Default is `/tablet`. Some servers also wire a tablet item that opens the same UI — both routes work in parallel.

### `ViewRepairZonesCommand`

Default is `/viewzones`. Renders all `repairZones` polygons in 3D at the nearest shop, including ground and ceiling. Used while configuring zones in custom MLOs to verify polygon points and ceiling detection.

## Aliases / Custom Names

Renaming any command updates the registered command immediately on resource start. So setting:

```lua
Config.UseTabletCommand = "mechanictablet"
```

Means players type `/mechanictablet` instead of `/tablet`. Useful if you have command-name collisions with other resources.

## Permission Layer

All admin commands check ACE permissions via the framework's standard admin check. The exact permission name matches the standard "is admin" predicate of your framework — no separate ACE setup needed.
