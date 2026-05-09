# Posts, Likes & Paywalls

## Post Types

A Fanly post is one of three:

* **Free** — anyone can see, like, comment, and share.
* **Subscriber** — anyone can see the preview, but full content requires an active subscription.
* **Pay-per-view (PPV)** — has its own per-post price on top of (or instead of) a subscription. Once unlocked, it stays unlocked for that fan permanently.

A post can carry text, an image, or a video (or a combination). Images and videos are validated against an extension whitelist server-side.

## Locked Posts

Locked posts show as a blurred preview with a lock badge and the unlock price. Tap to open the unlock sheet — confirm and the charge runs against your bank, then the content unlocks immediately.

Unlocks are permanent. If your subscription later expires, your previously unlocked PPV posts stay unlocked.

## Likes, Bookmarks & Shares

* **Like** — taps add to the like counter. Likes are public on the post but the list of who liked is not exposed.
* **Bookmark** — saves the post privately to your Bookmarks list.
* **Share** — copies the post link or shares to a DM thread.
* **Comment** — leave a text comment. Creators see all comments and can delete them.

Likes / comments / bookmarks / shares are gated by access state — you must hold the relevant unlock to engage with a locked post.

## Comments

Open a post to see the comment thread. Comments are chronological. The creator can delete any comment on their own post. Long comments are clamped to the configured max length (no spam-walls).

## Engagement Affects the Feed

Every interaction quietly tunes the recommender:

* Liking, sharing, bookmarking, commenting, unlocking, subscribing, or tipping a creator **increases** their affinity score for you.
* Hiding a post or unliking / unbookmarking **decreases** it.

Over time the feed leans toward the creators you actually engage with.
