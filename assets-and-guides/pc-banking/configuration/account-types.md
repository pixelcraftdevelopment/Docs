# Account Types

Defined in `pc-banking/config/accounts.lua`. Each type combines class, limits, fees, transfer/card/member permissions, and optional savings lock rules.

## Schema

```lua
Config.AccountTypes = {
    ['<typeKey>'] = {
        label               = 'Display Name',
        accountClass        = 'personal',      -- personal | shared | business
        autoCreateOnRegister= false,           -- usually true only for default checking types
        maxPerPlayer        = 1,               -- per player, per bank, for this exact type key

        canHaveCards        = true,
        canReceiveTransfers = true,
        canSendTransfers    = true,
        canAddMembers       = false,           -- shared/business feature gate
        maxMembers          = 0,               -- used when canAddMembers = true
        canAutoPay          = false,           -- standing orders
        maxStandingOrders   = 0,
        canPayroll          = false,           -- role-recipient standing orders

        interestRate        = 0,
        minBalance          = 0,
        maxBalance          = 0,               -- 0 or nil = unlimited
        depositLimit        = 0,               -- per transaction
        withdrawLimit       = 0,               -- per transaction
        dailyTransactionLimit = 0,             -- per-account tx count/day

        openingFee          = 0,
        monthlyFee          = 0,
        minOpeningDeposit   = 0,
        transferFee         = 0,
        freeATMWithdrawals  = 0,
        atmWithdrawalFee    = 0,

        withdrawalCooldown  = 0,               -- seconds (savings withdrawal flow)
        earlyWithdrawalPenalty = 0,            -- percent
        lockInDays          = 0,               -- days
    },
}
```

## Field Reference

### Identity and Provisioning

| Field | Type | Notes |
|-------|------|-------|
| `label` | string | Display name shown across UI/account details |
| `accountClass` | string | One of `'personal'`, `'shared'`, `'business'` |
| `autoCreateOnRegister` | bool | Marks types intended to be auto-opened during registration/primary-account setup; also hidden from manual savings type picker |
| `maxPerPlayer` | number | Max accounts of this type a player can open **per bank** (`owner + account_type + bank_name`) |

### Access and Capability Flags

| Field | Type | Notes |
|-------|------|-------|
| `canHaveCards` | bool | If `false`, card issuance from this account type is blocked |
| `canReceiveTransfers` | bool | If `false`, inbound transfers to this type are rejected |
| `canSendTransfers` | bool | If `false`, outgoing account-based transfers are blocked |
| `canAddMembers` | bool | Enables member management on shared/business accounts |
| `maxMembers` | number | Member cap when `canAddMembers` is enabled |
| `canAutoPay` | bool | Allows this account type to create standing orders |
| `maxStandingOrders` | number | Max active/paused standing orders on this account (`0` = unlimited) |
| `canPayroll` | bool | Allows standing orders with `recipientType = 'role'` (payroll-style payments) |

### Balances, Interest, and Limits

| Field | Type | Notes |
|-------|------|-------|
| `interestRate` | number | Annual percent rate stored on account creation; used for periodic accrual |
| `minBalance` | number | Withdrawal floor used in savings withdrawal paths (prevents dropping below this balance) |
| `maxBalance` | number \| nil | Credit cap. `0`/`nil` = unlimited; otherwise deposits/transfers/credits that exceed cap are rejected |
| `depositLimit` | number | Per-transaction deposit cap (`0`/`nil` disables the account-level cap) |
| `withdrawLimit` | number | Per-transaction withdrawal cap (`0`/`nil` disables the account-level cap) |
| `dailyTransactionLimit` | number | Max transaction count per account per calendar day (`DATE(created_at)=CURDATE()`) |

### Fees and ATM Behavior

| Field | Type | Notes |
|-------|------|-------|
| `openingFee` | number | Charged when opening this account type |
| `monthlyFee` | number | Periodic maintenance fee (interval from `Config.MonthlyFeeInterval`) |
| `minOpeningDeposit` | number | Minimum initial deposit required when opening this type (flow-dependent for primary creation) |
| `transferFee` | number | Added to outgoing **account-source** transfers |
| `freeATMWithdrawals` | number | Daily free ATM withdrawals before charging `atmWithdrawalFee` |
| `atmWithdrawalFee` | number | Per-withdraw ATM fee after free quota is exhausted |

### Savings Lock and Cooldown Controls

| Field | Type | Notes |
|-------|------|-------|
| `withdrawalCooldown` | number | Cooldown in seconds between savings withdrawals from the same account |
| `earlyWithdrawalPenalty` | number | Penalty percent charged on savings withdrawals/closure before lock-in expiry |
| `lockInDays` | number | Lock period in days from account creation |

## Behavior Notes

1. `transferFee` and `canSendTransfers` are enforced on account-source transfers; card-source nearby transfers intentionally skip those account-only checks.
2. `dailyTransactionLimit` checks transaction row count for that account/day, not daily money volume.
3. `maxBalance` is enforced as a hard cap anywhere the account is credited (deposit, transfer in, interest, refunds, etc.).
4. `interestRate` accrual job currently selects `checking*` and `savings*` account keys; shared/business types do not accrue unless server logic is extended.
5. ATM fee charging requires both quota and fee to be meaningful for your design (configure both fields intentionally).

## Account Classes

### `personal`
Single-owner account. No member system.

### `shared`
Multi-user account with member permissions.

### `business`
Business/society-oriented account type (often used with payroll and role workflows).

## Permissions (shared/business)

| Permission | Can View | Can Deposit | Can Withdraw | Can Manage Members |
|-----------|----------|-------------|--------------|---------------------|
| `view`    | yes      | no          | no           | no                  |
| `deposit` | yes      | yes         | no           | no                  |
| `full`    | yes      | yes         | yes          | no                  |
| `admin`   | yes      | yes         | yes          | yes                 |

Owner always has implicit admin permission regardless of stored permission.

## Required Type Definitions

Each bank needs at minimum a checking type matching its `defaultCheckingType` in `Config.Banks`. Shared/business naming convention is typically `shared_<bankId>` and `business_<bankId>`.
