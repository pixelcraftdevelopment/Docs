# Banking Password / Login

```lua
Config.RequireBankingPassword = true
Config.MinPasswordLength      = 4
Config.SessionDurationHours   = 24
```

## Field Behavior

| Field | Type | Behavior |
|-------|------|----------|
| `RequireBankingPassword` | bool | If `false`, auth check returns `passwordRequired = false` and the player enters directly. |
| `MinPasswordLength` | number | Minimum length enforced during registration/password set. |
| `SessionDurationHours` | number | Session-token expiry window in hours. If `<= 0`, token is stored with no expiry timestamp. |

## Notes

1. Passwords are stored as hashes.
2. Session token validation also checks bank context (`bank_id`) and token ownership rules.
3. If password is disabled, token/password flow is bypassed for bank entry.
