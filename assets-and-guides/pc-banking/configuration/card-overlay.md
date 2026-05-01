# Card Overlay

Visual overlay shown when a player uses a card item from inventory.

```lua
Config.CardOverlayPosition = 'bottom-left'  -- 9 anchor positions
Config.CardOverlayDuration = 8              -- seconds before auto-hide; 0 = manual dismiss only
```

## Positions

| Value |
|-------|
| `top-left`, `top-center`, `top-right` |
| `center-left`, `center`, `center-right` |
| `bottom-left`, `bottom-center`, `bottom-right` |

## Disabling

```lua
Config.CardOverlayDuration = 0   -- requires manual dismiss
```

To disable the overlay entirely, edit the card item's `useable` handler to skip the overlay trigger.
