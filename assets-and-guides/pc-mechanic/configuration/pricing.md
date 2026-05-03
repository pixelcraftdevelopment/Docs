# Pricing Engine

```lua
Config.VehcilePricingInParts = true
Config.AlwaysProfit          = true
Config.ProfitMargin          = false
Config.MinimumProfitBuffer   = 1
Config.UseLowestShopPrice    = false
```

| Field | Purpose |
|-------|---------|
| `VehcilePricingInParts` | If true, price scales with vehicle value via per-mod `vehiclevaluePortion` |
| `AlwaysProfit` | Ensures every sale produces a profit over the cost basis |
| `ProfitMargin` | Minimum profit % to enforce. `false` = use `MinimumProfitBuffer` instead |
| `MinimumProfitBuffer` | Flat buffer % above cost when `ProfitMargin = false` |
| `UseLowestShopPrice` | When the same item is sold across multiple shops, use lowest (`true`) or highest (`false`) as the reference |

## Two Pricing Modes

### Profit Margin Mode

```lua
Config.AlwaysProfit  = true
Config.ProfitMargin  = 25     -- always sell at 25% above cost minimum
```

The system enforces a 25% margin above cost — even if the configured price is lower, it lifts the price to maintain profit.

### Buffer Mode

```lua
Config.AlwaysProfit         = true
Config.ProfitMargin         = false
Config.MinimumProfitBuffer  = 1     -- 1% above cost minimum
```

Same idea, but the floor is `MinimumProfitBuffer` % above cost. Cleaner for servers where prices are already balanced and you just want a paper-thin "never sell at a loss" guard.

### No Profit Enforcement

```lua
Config.AlwaysProfit = false
```

Prices are exactly what's configured. A loss-making sale is allowed.

## Vehicle Value Scaling

Each `Config.ShopLocations[shop].mods[category]` block has:

- `price` — base price
- `vehiclevaluePortion` — fraction of vehicle value added on top
- `multiplier` (where present) — additional category-specific multiplier

When `VehcilePricingInParts = true`:

```
finalPrice = (basePrice + vehicleValue × vehiclevaluePortion) × (multiplier if present)
```

Then the profit guard layers on top. So a $100k car visiting Benny's for performance work pays:

```
8000 + 100000 × 0.01 = 9000 (base + value)
9000 × 1.15 = 10350 (multiplier applied)
```

Plus profit guard ensures it's at least `cost × (1 + margin)`.

When `VehcilePricingInParts = false`, `vehiclevaluePortion` is ignored — only `price` (and `multiplier`) apply. Useful for flat-rate shops.

## Cross-Shop Reference

`UseLowestShopPrice` only applies when the system needs a "what's this part worth" reference price across multiple shops:

- `true` — uses the cheapest configured price across all shops
- `false` — uses the highest

Most servers leave this at `false` (highest) so quoted prices favour the shop. Set to `true` for racing-style economies where the customer always gets the cheapest available rate.

## Interactions

### With Society Pay & Free Service

Pricing happens **before** payment routing. Society pay (`allowSocietyPay`) and free service (`allowFreeService`) operate on the final price:

- Society pay → final price comes out of society funds (gated by both shop and role flags)
- Free service → final price is zeroed entirely (gated by both shop and role flags, and `Config.SocietyMoneyAccess`)

### With Tablet Invoices

When a mechanic builds a work order in the tablet, the system computes per-category prices using this engine and presents them to both mechanic and customer. The customer pays the totalled invoice via:

- `Config.PlayerBalance` account type (default `"bank"`)
- Or society pay if both flags allow

### With Walk-Up Parts Shops

Walk-up parts shop prices (`Config.ShopLocations[shop].shops[].items[].price`) **do not** go through the pricing engine. They're flat counter prices set per shop. The engine only applies to mod/tuning installation pricing, not to over-the-counter part sales.
