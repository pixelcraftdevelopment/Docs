# Auto-Payments

Automatic scheduled payment controls in `pc-banking/config/config.lua`.

```lua
Config.AutoPayLoans                 = true
Config.LoanAutoPayAllAccountsFallback = true
Config.AutoPayCreditCards           = true
Config.CreditCardFreezeAfterMisses  = 3
Config.CreditCardDefaultAfterMisses = 6
```

## Field Behavior

| Field | Type | Behavior |
|-------|------|----------|
| `AutoPayLoans` | bool | If true, scheduler attempts to pay overdue EMIs from the resolved loan account balance. |
| `LoanAutoPayAllAccountsFallback` | bool | When the loan's bound account cannot pay, tries the player's other owned accounts, then online cash. |
| `AutoPayCreditCards` | bool | If true, scheduler attempts to auto-pay due credit-card minimums. |
| `CreditCardFreezeAfterMisses` | number | Consecutive missed minimums before card is frozen. |
| `CreditCardDefaultAfterMisses` | number | Consecutive missed minimums before card debt is written off/defaulted. |

## Notes

1. Loan default threshold is controlled separately by `Config.DefaultAfterOverdueEMIs`.
2. Auto-pay disabled means no automatic deduction attempts; overdue/default lifecycle rules still apply.
