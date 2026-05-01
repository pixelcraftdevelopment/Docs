# Banks

Defined in `pc-banking/config/banks.lua`. Each bank is a brand with its own account/card/loan availability. Three banks ship by default; add or remove freely.

## Schema

```lua
Config.Banks = {
    ['<bankId>'] = {
        label                 = 'Display Name',
        logo                  = 'logoKey',          -- maps to UI asset
        ibanPrefix            = 'XX',               -- 2-char prefix on account numbers
        defaultCheckingType   = 'checking_<bank>',  -- account type opened on first login
        availableAccountTypes = { ... },             -- subset of Config.AccountTypes keys
        availableCardTypes    = { ... },             -- subset of Config.CardTypes keys
        availableLoanTypes    = { ... },             -- subset of Config.LoanTypes keys
    },
}

Config.DefaultBank = 'fleeca'
```

## Field Reference

| Field | Type | Notes |
|-------|------|-------|
| `label` | string | Bank display name shown in UI and location context |
| `logo` | string | Logo key used by web/phone banking UI assets |
| `ibanPrefix` | string | Prefix used when generating account numbers for that bank |
| `defaultCheckingType` | string | Account type auto-selected for first primary checking at this bank |
| `availableAccountTypes` | table | Whitelist of account type keys available at this bank |
| `availableCardTypes` | table | Whitelist of card type keys issueable at this bank |
| `availableLoanTypes` | table | Whitelist of loan type keys offerable at this bank |
| `Config.DefaultBank` | string | Global fallback bank id for remote/default contexts |

## Behavior Notes

1. Each list field is an allowlist; missing keys are hidden/rejected even if defined elsewhere.
2. `defaultCheckingType` should point to a valid key in `Config.AccountTypes` and should usually be present in `availableAccountTypes`.
3. ATM/bank context fallbacks use `Config.DefaultBank` when a specific branch/bank cannot be resolved.

## Default Banks

### Fleeca
Neighborhood budget bank. Most accessible.

```lua
['fleeca'] = {
    label    = 'Fleeca',
    logo     = 'fleeca',
    ibanPrefix = 'FL',
    defaultCheckingType  = 'checking_fleeca',
    availableAccountTypes = { 'checking_fleeca', 'savings_fleeca_basic', 'shared_fleeca', 'business_fleeca' },
    availableCardTypes    = { 'standard', 'gold' },
    availableLoanTypes    = { 'personal', 'vehicle' },
},
```

### Maze Bank
Corporate mid-premium. Business focus.

```lua
['maze'] = {
    label    = 'Maze Bank',
    logo     = 'maze',
    ibanPrefix = 'MZ',
    defaultCheckingType  = 'checking_maze',
    availableAccountTypes = { 'checking_maze', 'savings_maze_growth', 'savings_maze_business', 'shared_maze', 'business_maze' },
    availableCardTypes    = { 'standard', 'maze', 'maze_gold' },
    availableLoanTypes    = { 'personal', 'vehicle', 'business' },
},
```

### Pacific Standard
Flagship prestige. Best rates and limits.

```lua
['pacific'] = {
    label    = 'Pacific Standard',
    logo     = 'pacific',
    ibanPrefix = 'PS',
    defaultCheckingType  = 'checking_pacific',
    availableAccountTypes = { 'checking_pacific', 'savings_pacific_vault', 'savings_pacific_elite', 'shared_pacific', 'business_pacific' },
    availableCardTypes    = { 'standard', 'platinum', 'shark', 'pacific_black' },
    availableLoanTypes    = { 'personal', 'vehicle', 'property', 'business' },
},
```

## Adding a New Bank

1. Add a row to `Config.Banks` with a unique key
2. Add bank-specific account types under `Config.AccountTypes` (suffix the key with the bank id)
3. Set `availableAccountTypes` / `availableCardTypes` / `availableLoanTypes` to the keys you want to expose
4. Add a logo asset in `pc-banking/web/dist/assets/` and `pc-banking-phone/ui/public/banks/`
5. Restart the resource

{% hint style="warning" %}
Removing a bank that has live customer accounts will break those accounts at runtime. Migrate balances out first, or keep the bank entry but set every `availableAccountTypes` to `{}` to prevent new openings.
{% endhint %}
