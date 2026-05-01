# Two-Factor Authentication

OTP controls in `pc-banking/config/config.lua`.

## Schema

```lua
Config.TwoFactorEnabled                 = true
Config.TwoFactorTransferThreshold       = 10000
Config.TwoFactorSocietyThreshold        = 25000
Config.TwoFactorAlwaysForPassword       = true
Config.TwoFactorAlwaysForCardManagement = true
Config.TwoFactorOTPExpiry               = 300
Config.TwoFactorMaxAttempts             = 3
Config.TwoFactorCooldown                = 30
```

## Field Reference

| Field | Type | Runtime Behavior |
|-------|------|------------------|
| `TwoFactorEnabled` | bool | Master gate for OTP generation/verification paths. |
| `TwoFactorTransferThreshold` | number | Transfer flow checks this threshold (`amount >= threshold`) before entering OTP path. |
| `TwoFactorSocietyThreshold` | number | Society flow checks this threshold (`amount > threshold`) before entering OTP path. |
| `TwoFactorAlwaysForPassword` | bool | Password-change flow enters OTP path when true. |
| `TwoFactorAlwaysForCardManagement` | bool | Card lock/PIN/reset/limit flows enter OTP path when true. |
| `TwoFactorOTPExpiry` | number | OTP validity window in seconds. |
| `TwoFactorMaxAttempts` | number | Max wrong verification attempts before OTP entry is cleared. |
| `TwoFactorCooldown` | number | Per-identifier cooldown (seconds) between OTP generations. |

## Important Runtime Note

OTP generation for standard flows uses the profile's `two_factor_enabled` flag. So threshold/always checks route into OTP logic, but an OTP is only issued when that profile flag is enabled (unless a special admin-fanout OTP path is used).

## Delivery Path

Standard OTP delivery is via `PhoneBridge.SendSMS(...)` when phone bridge is available.
