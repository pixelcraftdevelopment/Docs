# Platform Fee

The percentage taken from every creator credit before it lands in their wallet — a money sink for the server economy.

```lua
Config.PlatformFeePct = 10   -- 0..50 percent
```

## How It Works

Every charge a fan pays — sub, tip, PPV unlock, paid DM — credits the creator's wallet **after** the platform fee is deducted. Example with the default 10%:

| Fan pays | Platform takes | Creator gets |
|----------|----------------|--------------|
| $10 sub | $1 | $9 |
| $50 tip | $5 | $45 |
| $20 PPV unlock | $2 | $18 |

## Range

`0` to `50`. Set to `0` to disable the fee entirely. Above 50 the value is clamped server-side.

## Tuning

* **5-10%** — light tax, mainly for flavour. Most earnings flow to creators.
* **15-25%** — meaningful sink. Discourages money pumping via Fanly trades while still leaving creators well-paid.
* **30-50%** — heavy sink. Use when Fanly is identified as a money inflation vector on your server.
