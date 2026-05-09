# Push Channel & Sender Labels

Controls how outbound notifications are branded.

## Sender Labels

These appear on the SMS / mail / native push that lands on a player's phone:

```lua
Config.SmsSender         = 'Fanly'
Config.MailSender        = 'noreply@fanly.gg'
Config.MailSenderDisplay = 'Fanly'
```

| Key | Where It Shows | Default |
|-----|----------------|---------|
| `SmsSender` | SMS sender name in the phone's messages app | `Fanly` |
| `MailSender` | From-address on email notifications | `noreply@fanly.gg` |
| `MailSenderDisplay` | Display name for the email sender | `Fanly` |

Change these to match your server's brand.

## Push Channel

```lua
Config.PushChannel = 'fanly:push'
```

Internal channel name used for live UI refresh events. You generally don't need to change this — only relevant if you're integrating Fanly with a custom dashboard or analytics layer that subscribes to the same channel.

## What Triggers a Push

Every notable event sends both an in-app notification and an outbound phone push:

* New subscriber
* Subscription renewed / expired / renewal failed
* Tip received
* PPV post unlocked
* New direct message
* New comment on your post
* New post from a creator you follow
* Withdraw to bank confirmed

The exact format (SMS vs mail vs native popup) is decided by the active phone resource — Fanly hands the message off and the phone host renders it.
