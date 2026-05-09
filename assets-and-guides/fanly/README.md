# Fanly

{% hint style="info" %}
Standalone creator-subscription phone app for FiveM. Subscribers, paid posts, tips, paid DMs, and creator earnings — all on the in-game phone.
{% endhint %}

## Description

Fanly is a self-contained creator-economy app that lives inside any modern FiveM phone. Players can follow creators, subscribe monthly, unlock pay-per-view posts, send tips, and chat in paid DMs. Creators get a Studio dashboard with earnings, payout history, and pricing controls.

The resource ships as a single phone app — no desktop UI. It runs on **lb-phone**, **yseries**, **gksphone**, **qs-smartphone** (and pro), **qb-phone**, **17mov_Phone**, and **npwd**, and registers itself against whichever one is started.

## Features

* Creator profiles with handle, display name, bio, avatar, banner, and DM permission
* Single base monthly subscription price per creator (OnlyFans-style, not Patreon-tier)
* Bundles — same access, longer commitment with a percentage discount (3 / 6 / 12 month)
* Free trial — one-time per fan, configurable length
* Time-bounded promo discount on the first month
* Pay-per-view posts with per-post pricing
* Free post mode for previews and lead-in content
* Likes, bookmarks, comments, shares — gated by unlock state
* Tips on profiles, posts, and inside DMs
* Direct messages with optional paid-message gating
* Studio dashboard — earnings, payout history, post history, fan count
* Withdraw earnings to bank (auto-detects pc-banking, qb-banking, okokBanking, Renewed-Banking, wasabi, jaksam, fd, tgg, crm, prism, p_banking, justbanks, RxBanking, esx_addonaccount, or framework-native)
* Configurable platform fee (server money sink)
* Live phone push for new subs, tips, unlocks, DMs, comments, renewals, expiries
* Notifications app history with read state
* Cross-account sign-in — type a friend's creds on your phone and you become them for the session (own posts/DMs/earnings stay attributed correctly)
* Forgot password via SMS code, routed to the account owner's phone
* Persistent 24-hour session tokens (own-account only — leaked tokens never resume someone else's account)
* Deterministic feed ranking with freshness, engagement, affinity, popularity, fatigue
* 10 locales: en, es, fr, de, it, pt, sv, ja, cn, ar
* Pure black OnlyFans-inspired theme with signature blue accent

## Guides

* [Installation](installation.md)
* [Fanly Guide](guide/README.md)
* [Configuration](configuration/README.md)
