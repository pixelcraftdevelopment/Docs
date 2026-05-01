# Backwards Compatibility Shims

Legacy-export shim toggles in `pc-banking/config/config.lua`.

## Schema

```lua
Config.Compat = {
    qb_banking               = 'auto',
    qb_management            = 'auto',
    renewed_banking          = 'auto',
    esx_addonaccount         = 'auto',
    esx_society              = 'auto',
    okok_banking             = 'auto',
    qs_banking               = 'auto',
    tgg_banking              = 'auto',
    rx_banking               = 'auto',
    omes_banking             = 'auto',
    fd_banking               = 'auto',
    legacy_qb_banking_events = false,
}
```

## Runtime Behavior

For each compat key (except `legacy_qb_banking_events`):

- `false` or `nil`: shim disabled
- any other value (including `'auto'` and `true`): shim enabled

`legacy_qb_banking_events` is only enabled when explicitly set to `true`.

## Practical Note

Current shim gate does not perform per-resource `GetResourceState(...)` checks for `Config.Compat.*` values. If you want a shim off, set it to `false` explicitly.
