# Card Types

Defined in `pc-banking/config/cards.lua`. Each card type controls visuals, issuance limits, lock/PIN controls, and credit behavior.

## Schema

```lua
Config.CardTypes = {
    ['<cardTypeKey>'] = {
        label               = 'Display Name',
        network             = 'Network Name',
        cardMode            = 'debit',      -- debit | credit

        icon                = 'icon_key',   -- file name (without extension)
        iconExt             = 'png',
        color               = '#1a1f71',
        gradient            = { from = '#1e40af', to = '#3b82f6' },

        itemName            = 'card_item_key',

        monthlyLimitDefault = 5000,
        monthlyLimitMax     = 15000,        -- 0 = unlimited
        dailyWithdrawLimit  = 1500,

        issuanceFee         = 0,
        annualFee           = 0,
        transactionFee      = 0,
        expiryYears         = 3,

        canFreeze           = true,
        canChangePIN        = true,
        maxPerAccount       = 2,

        -- credit-mode only
        creditLimit         = 50000,
        creditInterestRate  = 18.0,
        minPaymentPercent   = 10,
    },
}
```

## Field Reference

### Identity

| Field | Type | Notes |
|-------|------|-------|
| `label` | string | Display name in issue/select screens |
| `network` | string | Network/brand text shown on card UI |
| `cardMode` | string | `'debit'` or `'credit'` |

### Visuals

| Field | Type | Notes |
|-------|------|-------|
| `icon` | string | Card icon key from `web/dist/assets/cardIcons/` |
| `iconExt` | string | Icon file extension (usually `png`) |
| `color` | string | Primary color used by card UI |
| `gradient` | table | `{ from, to }` background gradient colors |

### Inventory and Issuance

| Field | Type | Notes |
|-------|------|-------|
| `itemName` | string | Inventory item name used for physical card issuance/usability |
| `maxPerAccount` | number | Max cards of this type per account (owner/account/type/bank scoped) |
| `expiryYears` | number | Card expiry horizon in game-years (`Config.AnnualFeeInterval` scale) |

### Spending Limits

| Field | Type | Notes |
|-------|------|-------|
| `monthlyLimitDefault` | number | Starting monthly spend cap when card is created |
| `monthlyLimitMax` | number | Highest monthly cap owner can set later (`0` = unlimited) |
| `dailyWithdrawLimit` | number | ATM daily withdraw cap for debit-mode withdrawals |

### Fees

| Field | Type | Notes |
|-------|------|-------|
| `issuanceFee` | number | One-time issue fee charged at card creation |
| `annualFee` | number | Recurring fee charged on `Config.AnnualFeeInterval` |
| `transactionFee` | number | Reserved field in current build (not applied by runtime yet) |

### Security Controls

| Field | Type | Notes |
|-------|------|-------|
| `canFreeze` | bool | If `false`, manual lock/unlock action is blocked for this type |
| `canChangePIN` | bool | If `false`, PIN-change action is blocked for this type |

### Credit-Mode Fields

| Field | Type | Notes |
|-------|------|-------|
| `creditLimit` | number | Max revolving balance for credit cards |
| `creditInterestRate` | number | APR used in billing-cycle interest accrual |
| `minPaymentPercent` | number | Percent of outstanding credit balance due as minimum payment |

## Behavior Notes

1. `itemName` also drives `ATMRequiresCard` checks and inventory-based ATM usage.
2. `monthlyLimit` enforcement applies to card spend/withdraw charges (amount side; fees are tracked separately in ATM fee paths).
3. Credit cards still use `monthlyLimitDefault`/`monthlyLimitMax` in addition to `creditLimit`.
4. `dailyWithdrawLimit` is enforced for non-credit ATM withdrawals.

## Default Card Types

| Key | Mode | Network | Monthly Default | Monthly Max | Credit Limit |
|-----|------|---------|-----------------|-------------|--------------|
| `standard` | debit | iFruit | 5,000 | 15,000 | n/a |
| `gold` | debit | Fleeca | 10,000 | 40,000 | n/a |
| `maze` | debit | Maze Bank | 15,000 | 75,000 | n/a |
| `maze_gold` | credit | Maze Bank | 25,000 | 150,000 | 50,000 |
| `platinum` | credit | Lombank | 50,000 | 500,000 | 200,000 |
| `shark` | credit | Shark | 100,000 | 1,000,000 | 500,000 |
| `pacific_black` | credit | Pacific Standard | 250,000 | unlimited | 2,000,000 |
