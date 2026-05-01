# Phone Integration

Phone bridge settings in `pc-banking/config/config.lua`.

## Schema

```lua
Config.Phone                      = 'auto'   -- 'auto' | 'lb-phone' | 'qs-smartphone' | 'qs-smartphone-pro' | 'qb-phone' | 'npwd' | 'gksphone' | 'yseries' | '17mov_Phone' | false
Config.PhoneNotifications         = true
Config.PhoneSMSForTransfers       = true
Config.PhoneSMSForSecurity        = true
Config.PhoneSMSForEMI             = true
Config.PhoneLargeTransactionAlert = true
```

## Field Behavior

| Field | Type | Behavior |
|-------|------|----------|
| `Phone` | string/bool | Selects phone provider. `false` disables provider detection/use. `'auto'` picks first started provider from runtime priority list. |
| `PhoneNotifications` | bool | Controls phone push notifications sent via `PhoneBridge.SendPushNotification(...)` from notification flow. |
| `PhoneSMSForTransfers` | bool | Enables transfer SMS notifications where transfer flows call `SendSMS`. |
| `PhoneSMSForSecurity` | bool | Enables security/auth/card SMS/push paths that check this flag. |
| `PhoneSMSForEMI` | bool | Enables EMI-related SMS notifications in loan scheduler paths. |
| `PhoneLargeTransactionAlert` | bool | Enables large-transfer SMS alert path (threshold uses `Config.WebhookThreshold`). |

## Auto-Detect Order

When `Config.Phone = 'auto'`, runtime checks providers in this order:

1. `lb-phone`
2. `qs-smartphone`
3. `qs-smartphone-pro`
4. `qb-phone`
5. `npwd`
6. `gksphone`
7. `yseries`
8. `17mov_Phone`
