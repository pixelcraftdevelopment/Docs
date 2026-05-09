# Notifications

## In-App Notifications

The **bell** icon in the top bar opens your notifications list — a chronological history of everything Fanly has pinged you about. Tap any item to jump straight to the relevant post, thread, or profile.

Notification kinds you'll see:

| Kind | When |
|------|------|
| **New subscriber** | A fan subscribes to you (monthly, bundle, or trial) |
| **Subscription renewed** | An auto-renewal succeeds |
| **Subscription expired** | A fan's sub ran out (or yours did) |
| **Renewal failed** | A renewal hit insufficient funds |
| **Tip received** | A fan tipped you |
| **PPV unlocked** | A fan paid to unlock one of your posts |
| **DM received** | New incoming direct message |
| **New post** | A creator you follow posted |
| **New comment** | Someone commented on one of your posts |
| **Withdraw confirmed** | A payout to bank completed |

## Phone Pushes

The same events also send a push to your phone — surfaced as an SMS, mail, or native push depending on which phone resource is running:

* **lb-phone** — uses the SMS app + native push.
* **yseries** — uses SMS + mail.
* **gksphone / qs-smartphone / qb-phone / 17mov_Phone / npwd** — use the host's native notification system.

## Live Refresh

When a push arrives while the app is open, the relevant screen reloads in the background — you don't need to pull-to-refresh.

## Read State

Opening a notification marks it read. The bell badge counts unread items only.

## Customising

The sender labels (SMS sender name, mail sender address) are server-configurable for rebrands. Defaults:

* SMS sender: `Fanly`
* Mail sender: `noreply@fanly.gg`
