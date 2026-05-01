# PushToAppForIdentifier

Same as [`PushToApp`](PushToApp.md) but resolves identifier → server src internally. No-op if the identifier is offline.

```lua
exports['pc-banking-phone']:PushToAppForIdentifier(identifier, kind, payload)
```

| Param | Type | Notes |
|-------|------|-------|
| `identifier` | string | Player identifier |
| `kind` | string | Event kind (see [PushToApp](PushToApp.md#common-kinds)) |
| `payload` | table | Free-form payload |

## Example

```lua
exports['pc-banking-phone']:PushToAppForIdentifier(borrowerIdent, 'loans:changed', {
    reason = 'disbursed',
    amount = 50000,
})
```

## Notes

* For account-scoped fan-out (push to every member of a shared/business account), call this for each member identifier — there is no built-in fan-out export.
