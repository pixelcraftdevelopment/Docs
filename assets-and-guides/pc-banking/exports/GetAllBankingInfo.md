# GetAllBankingInfo

**Side:** Server

Read a player's accounts, cards, and per-bank loan availability. Read-only — no mutations.

## Signature

```lua
local res = exports['pc-banking']:GetAllBankingInfo(target)
```

`target` accepts:

* **string** — player identifier (e.g. `'ABC123'`, `'license:abc...'`)
* **number** — player server src (e.g. `42`)
* **table** — `{ targetIdentifier = 'ABC123' }` or `{ targetSrc = 42 }` or `{ identifier = 'ABC123' }`

## Returns

```lua
{
    success        = true,
    identifier     = 'ABC123',
    accounts       = { ... },         -- see Account schema
    cards          = { ... },         -- see Card schema
    availableLoans = { ... },         -- see Loan schema, one row per (bank, loanType)
    hasAnyAccount  = true,
}
```

On failure: `{ error = true, message = '...' }`

### Account Schema

```lua
{
    id               = 17,
    accountType      = 'checking_fleeca',
    label            = 'Fleeca Checking',
    bankId           = 'fleeca',
    bankLabel        = 'Fleeca',
    last4            = '4892',
    isPrimary        = true,
    frozen           = false,
    accountClass     = 'personal',     -- 'personal' | 'shared' | 'business'
    memberPermission = nil,            -- nil = owner; 'view' | 'deposit' | 'full' | 'admin' otherwise
}
```

### Card Schema

```lua
{
    id          = 31,
    mode        = 'debit',             -- 'debit' | 'credit'
    bankId      = 'fleeca',
    bankLabel   = 'Fleeca',
    network     = 'visa',
    cardType    = 'standard',
    icon        = 'visa',
    iconExt     = 'png',
    gradient    = { from = '#1f2937', to = '#0f172a' },
    last4       = '8412',
    expiry      = '12/28',             -- mm/yy
    accountId   = 17,                  -- linked account, or nil for orphans
    locked      = false,
    expired     = false,
    creditLimit = nil,                 -- credit cards only
}
```

### Loan Schema

Same loan type can appear multiple times if offered by multiple banks. Each row carries that bank's scoped state.

```lua
{
    loanType           = 'personal',
    label              = 'Personal Loan',
    bankId             = 'fleeca',
    bankLabel          = 'Fleeca',
    minAmount          = 1000,
    maxAmount          = 100000,
    minTermMonths      = 1,
    maxTermMonths      = 24,
    interestRate       = 12.0,
    collateralPercent  = 0,
    requiresCollateral = false,
    minCreditScore     = 350,
    maxActiveLoans     = 3,
    earlyPayoffPenalty = 0,
    eligibleMax        = 87500,        -- credit-score-adjusted, exposure-adjusted
    eligibilityPct     = 88,           -- 0–100 (% of maxAmount)
    currentActive      = 1,            -- active loans of this type at this bank
    canApply           = true,
    targetHasAccount   = true,         -- target has at least one account at this bank
}
```

## Examples

### By Identifier

```lua
local res = exports['pc-banking']:GetAllBankingInfo('license:abc123')
if res and res.success then
    for _, acc in ipairs(res.accounts) do
        print(acc.bankLabel, acc.label, acc.last4)
    end
end
```

### By Server Src

```lua
local res = exports['pc-banking']:GetAllBankingInfo(source)
```

### Filter Loans by Bank

```lua
local res = exports['pc-banking']:GetAllBankingInfo(targetSrc)
local pacificLoans = {}
for _, loan in ipairs(res.availableLoans) do
    if loan.bankId == 'pacific' and loan.canApply then
        pacificLoans[#pacificLoans + 1] = loan
    end
end
```

## Notes

* Returns shared/business accounts where the target is a member. `memberPermission` field distinguishes (nil = owner).
* Cards include orphan cards (no linked account) at any bank where target has cards.
* Loan eligibility is bank-scoped per `Config.LoanExposureScope`. If set to `'global'`, `currentActive` and `eligibleMax` reflect cross-bank totals.
* Output contains NO balances — vendor scripts get account/card metadata only.
