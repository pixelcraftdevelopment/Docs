# Client Events

Client events are triggered from the server with `TriggerClientEvent(...)`. Use them when another resource needs to ask PC-Mechanic to run an existing client-side action for a specific player.

## Admin Repair

Repairs the player's vehicle using the same repair behavior as the internal admin repair command.

```lua
TriggerClientEvent("pc-mechanic:cl:execute-admin-repair", source)
```

| Argument | Type | Purpose |
|----------|------|---------|
| `source` | integer | Player server ID that should receive the repair event |

## Example

```lua
RegisterCommand("customfix", function(source)
    TriggerClientEvent("pc-mechanic:cl:execute-admin-repair", source)
end, true)
```

## Notes

- This is intended for admin or trusted integration flows.
- The event performs the same vehicle repair action used by the internal `fixpc` admin flow.
- Trigger the event for the player who should run the vehicle repair action on their client.
