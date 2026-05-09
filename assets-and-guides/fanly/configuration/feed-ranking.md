# Feed Ranking

The Home / Subscribed / Discover feeds are deterministically ranked on the server. Tune the weights here without touching UI code.

```lua
Config.Ranking = {
    enabled = true,

    candidateMultiplier = 8,
    minCandidates       = 320,
    maxConsecutiveCreator = 2,

    impressionCooldownSeconds    = 1800,
    viewerImpressionMaxPerMinute = 30,

    weights        = { ... },
    affinityDeltas = { ... },
}
```

## Master Switch

```lua
Config.Ranking.enabled = true   -- false = chronological feed only
```

Set to `false` to revert to a simple newest-first feed (no ranking, no affinity). Useful for low-content servers where there are not enough posts to rank.

## Candidate Pool

Feed queries pull a wider set of posts, rank and diversify them, then return the requested page.

| Key | What | Default |
|-----|------|---------|
| `candidateMultiplier` | Pool grows as `requested page size × this` | 8 |
| `minCandidates` | Floor on the pool — never query fewer than this | 320 |
| `maxConsecutiveCreator` | Most posts in a row from the same creator | 2 |

The candidate pool grows with page depth, so infinite scroll never stops at a hard cap.

## Impression Telemetry

Engagement signals depend on knowing what a viewer has already seen. The client reports a card impression once per visible card per app session, and the server cools down duplicates.

| Key | What | Default |
|-----|------|---------|
| `impressionCooldownSeconds` | Per-post cooldown before the same viewer's repeat impression counts again | 1800 (30 min) |
| `viewerImpressionMaxPerMinute` | Max distinct posts a single viewer can mark seen per minute. `0` disables | 30 |

## Weights

Higher = stronger boost. Negative weights are penalties.

```lua
weights = {
    -- Freshness (newer posts surface higher)
    freshness            = 140,
    freshnessOffsetHours = 2,
    freshnessDecayPower  = 1.18,

    -- Engagement signals
    like      = 8,
    comment   = 14,
    bookmark  = 16,
    share     = 18,
    open      = 7,
    ppvUnlock = 28,

    -- Relationship signals
    activeSubCreator  = 18,    -- viewer subscribes to this creator
    creatorAffinity   = 0.22,  -- multiplier on viewer↔creator affinity score
    creatorPopularity = 8,     -- multiplier on creator's broad popularity

    -- Monetisation tilt
    ppvPreview = 3,            -- locked PPV gets a small lift
    freePost   = 1,            -- unlocked posts get a tiny base lift

    -- Fatigue
    seenPenalty = 3,           -- per-prior-impression dampener
}
```

## Affinity Deltas

Every interaction nudges the viewer↔creator affinity score. Higher affinity → more of that creator's posts in the viewer's feed.

```lua
affinityDeltas = {
    impression = 0,    -- baseline (no change)
    open       = 1,
    share      = 5,
    like       = 2,
    unlike     = -1,
    bookmark   = 4,
    unbookmark = -2,
    comment    = 6,
    ppvUnlock  = 14,
    subscribe  = 18,
    tip        = 12,
    hide       = -24,  -- explicit "show less"
}
```

## Tuning Tips

* If users complain "I keep seeing the same creators" — drop `creatorAffinity` and `activeSubCreator`.
* If new creators struggle to surface — raise `freshness` and lower `creatorPopularity`.
* If too many locked PPV posts clutter the feed — drop `ppvPreview`.
* If users see posts they've already seen too often — raise `seenPenalty`.
