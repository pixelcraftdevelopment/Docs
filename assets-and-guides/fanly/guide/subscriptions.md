# Subscriptions, Bundles & Trials

Fanly uses a single base monthly price per creator. Bundles, trials, and promos all reskin that base price — they don't add separate "tiers" with different access. A subscriber gets the **same** content regardless of how they paid.

## The Four Subscription Types

| Type | What It Is | Auto-Renews? |
|------|------------|--------------|
| **Monthly** | Base price, charged each in-game month (~7 real days). | Yes |
| **Bundle 3-month** | 3 months prepaid with a discount. | No — fan resubscribes when it ends |
| **Bundle 6-month** | 6 months prepaid with a deeper discount. | No |
| **Bundle 12-month** | 12 months prepaid with the deepest discount. | No |
| **Free trial** | One-shot free access for N days (set by creator). | No — one per fan per creator, ever |

Only **Monthly** auto-renews. Every other tier ends cleanly when its term is up and the fan has to actively resubscribe.

## Promos

Creators can run a time-bounded promo — e.g. "50% off your first month, ends Friday". Promos apply only to the first monthly charge for **new** subscribers, not renewals or bundle purchases.

## How Renewal Works

A background renewer wakes up periodically and charges every active monthly sub. If the charge succeeds, the term extends. If it fails (insufficient funds), the sub is marked expired and both fan and creator get a notification.

* Default check cadence — once per in-game minute.
* Default monthly term — 7 real days = 1 in-game month.

Both are configurable server-side.

## Cancelling

You can cancel a subscription at any time from **Profile → Subscriptions**. Cancellation:

* Stops future auto-renewals.
* Leaves your current term active until the existing expiry date.
* Does not refund the current term.

When the term runs out, access drops to free posts only. PPV posts you previously unlocked stay unlocked forever.

## Pricing Caps

Servers cap the price ranges to keep the economy sane. Defaults:

| Setting | Default |
|---------|---------|
| Min monthly | $5 |
| Max monthly | $500 |
| Max bundle discount | 60% |
| Max trial length | 30 days |
| Max promo discount | 60% |

Per-bundle caps can be set independently — e.g. allow 60% off on 3-month, 70% on 6-month, 80% on 12-month.
