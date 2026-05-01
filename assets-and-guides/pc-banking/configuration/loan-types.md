# Loan Types

Defined in `pc-banking/config/loans.lua`. Loan products are global definitions; each bank chooses which ones to expose via `Config.Banks[bankId].availableLoanTypes`.

## Schema

```lua
Config.LoanTypes = {
    ['<loanTypeKey>'] = {
        label               = 'Display Name',
        interestRate        = 12.0,
        minAmount           = 1000,
        maxAmount           = 100000,
        minTermMonths       = 1,
        maxTermMonths       = 24,
        minCreditScore      = 350,
        requiresCollateral  = false,
        collateralPercent   = 0,
        earlyPayoffPenalty  = 0,
        allowSelfApply      = true,
        maxActiveLoans      = 3,
    },
}
```

## Loan Type Fields

| Field | Type | Notes |
|-------|------|-------|
| `label` | string | UI display name |
| `interestRate` | number | APR used in EMI and total-payable calculations |
| `minAmount` | number | Minimum principal allowed |
| `maxAmount` | number | Maximum principal allowed before eligibility trimming |
| `minTermMonths` | number | Shortest loan term accepted |
| `maxTermMonths` | number | Longest loan term accepted |
| `minCreditScore` | number | Required minimum score to apply |
| `requiresCollateral` | bool | Enables collateral lock on opening |
| `collateralPercent` | number | Percent of requested amount locked as collateral when enabled |
| `earlyPayoffPenalty` | number | Percent fee on remaining principal when paying off early |
| `allowSelfApply` | bool | If `false`, excluded from standard self-apply flow |
| `maxActiveLoans` | number | Max simultaneous active loans of this type (scope via `LoanMaxActiveScope`) |

## Credit Score Config

```lua
Config.CreditScore = {
    min = 300,
    max = 900,
    defaultForNew = 650,
    repaymentCapacity = 50000,
    ccWeight = 0.4,
    ccMaturityCycles = 12,
    ccMissedPenalty = 200,
    ccDebtMultiplier = 0.3,
}
```

| Field | Type | Notes |
|-------|------|-------|
| `min` | number | Floor score |
| `max` | number | Ceiling score |
| `defaultForNew` | number | Starting score for no-history players |
| `repaymentCapacity` | number | Confidence normalization volume for score/eligibility blending |
| `ccWeight` | number | Max share of repayment-capacity attributable to credit-card history |
| `ccMaturityCycles` | number | On-time cycles needed to unlock full CC contribution |
| `ccMissedPenalty` | number | History scar applied per missed CC payment |
| `ccDebtMultiplier` | number | Additional active-penalty multiplier on delinquent CC debt |

## Exposure and Scope

```lua
Config.LoanExposureScope  = 'bank'   -- bank | global
Config.LoanMaxActiveScope = 'bank'   -- bank | global
```

| Field | Notes |
|-------|-------|
| `LoanExposureScope` | Controls whether active exposure (remaining amount sum) is per-bank or global |
| `LoanMaxActiveScope` | Controls whether `maxActiveLoans` is counted per-bank or global |

## Default Lifecycle

```lua
Config.DefaultAfterOverdueEMIs = 3
```

After this many consecutive overdue EMIs, a loan is marked defaulted.

## Collateral and Write-Off Notes

1. Collateral is locked at origination if configured.
2. On recovery/closure/payoff paths, collateral is refunded (subject to destination cap handling).
3. Collateral is forfeited at write-off stage, not immediately at first default mark.
