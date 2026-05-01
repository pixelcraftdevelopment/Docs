# Fees & Charges

Static service fees in `pc-banking/config/config.lua`.

```lua
Config.Fees = {
    accountClosing  = 0,
    cardReplacement = 50,
    statementExport = 0,
}
```

## Field Reference

| Field | Type | Behavior |
|-------|------|----------|
| `accountClosing` | number | Charged by account-closing flow when closing savings/accounts. |
| `cardReplacement` | number | Charged in card replacement/reissue flow. |
| `statementExport` | number | Charged in statement export flow (`profile:exportStatements`, CSV export). |

Set a fee to `0` to disable that fee.
