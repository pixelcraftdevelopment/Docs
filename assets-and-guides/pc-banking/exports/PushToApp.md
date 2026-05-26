# PushToApp

**Side:** Server

Push a kind-tagged update to the `pc-banking-phone` app for a specific server src. Lives under the `pc-banking-phone` resource namespace.

```lua
exports['pc-banking-phone']:PushToApp(targetSrc, kind, payload)
```

| Param | Type | Notes |
|-------|------|-------|
| `targetSrc` | number | Server src of the player |
| `kind` | string | Event kind (see table) |
| `payload` | table | Free-form payload merged into the event body |

## Common Kinds

| Kind | Triggers In Phone App |
|------|---------------------|
| `requests:changed` | Refreshes Requests view + bumps inbox badge |
| `bills:changed` | Refreshes Bills view |
| `notif:new` | Shows toast immediately, regardless of current view |
| `account:balance` | Updates Home view balance ticker |
| `cards:changed` | Refreshes Cards view |
| `loans:changed` | Refreshes Loans view |
| `standing-orders:changed` | Refreshes Standing Orders view |

## Example

```lua
exports['pc-banking-phone']:PushToApp(playerSrc, 'notif:new', {
    title   = 'Loan approved',
    message = '$50,000 disbursed to your Fleeca primary',
    type    = 'success',
})
```

## Notes

* Requires `pc-banking-phone` to be running. Wrap in `GetResourceState('pc-banking-phone') == 'started'` for cross-server compatibility.
* Fire-and-forget. No delivery guarantee if phone app is closed; the app re-fetches on reopen.
