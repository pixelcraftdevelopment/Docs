# Overdraft

`Config.Overdraft` controls which accounts may have a negative balance and which debit paths may use that credit.

```lua
Config.Overdraft = {
    enabled = false,
    limit = 5000,
    eligibleAccountClasses = {
        personal = true,
        shared = false,
        business = false,
    },
    eligibleAccountTypes = {
        checking = true,
    },
    channels = {
        withdrawal = true,
        transfer = true,
        cardPurchase = true,
        external = true,
        atm = false,
        savings = false,
        accountOpening = false,
        loanPayment = false,
        creditPayment = false,
        standingOrder = false,
        fee = false,
        society = false,
        admin = false,
    },
}
```

| Field | Behavior |
|-------|----------|
| `enabled` | Master switch. When `false`, no account can use overdraft. |
| `limit` | Maximum negative balance, expressed as a positive amount. `5000` allows a balance down to `-5000`. |
| `eligibleAccountClasses` | Enables overdraft by account class. |
| `eligibleAccountTypes` | Enables overdraft by account type or its family prefix, such as `checking`. |
| `channels` | Enables it independently for each debit path. Disabled channels retain the normal non-negative-balance rule. |

An account type can further restrict this global policy with its own `overdraftEnabled` or `overdraftLimit` settings.

## QBCore Compatibility

QBCore must allow negative `bank` balances. If `QBCore.Config.Money.DontAllowMinus` contains `bank`, PC-Banking disables overdraft at runtime. The effective limit is also capped by QBCore's `Money.MinusLimit`; configure it as the same or a larger negative magnitude than `Config.Overdraft.limit`.
