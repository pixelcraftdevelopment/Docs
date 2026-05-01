# Loan Request (`loan_offer`)

Type key for `CreateRequest`: `loan_offer`

## Export Call

```lua
local requestId = exports['pc-banking']:CreateRequest(target, 'loan_offer', payload, opts)
```

## Important Flow Note

Loan request resolution does **not** originate principal by itself.

In the phone flow, loan application/disbursement happens before request resolution using `payload.applyArgs`. If `applyArgs` is wrong/missing, request resolution can still complete without the intended disbursement.

## Canonical Payload Shape

```lua
payload = {
  title = '...',
  subtitle = '...',
  amount = 50000,
  from = { name = issuerName, identifier = issuerIdentifier, avatar = 'AB' },
  actions = { 'accept', 'reject' },
  requiresAccount = false,
  applyArgs = {
    loanType = 'vehicle',
    termMonths = 24,
    bankId = 'maze',
  },
  destination = { kind = 'identifier' | 'account' | 'society', ... }, -- optional
  metadata = {
    apr = '6.5%',
    term = '24 mo',
    emi = 2227,
    total = 53448,
    collateral = 7500,
    bank = 'Maze Bank',
  },
  issuerIdentifier = 'char:issuer',
  issuerName = 'Vendor Name',
  bankId = 'maze',
}
```

## Field Reference

### Core offer fields

| Field | Type | Required | Validation / Behavior |
|-------|------|----------|-----------------------|
| `amount` | number | yes | Used by accept-side optional payout redirect logic; should match apply amount. |
| `title` | string | recommended | Request card title. |
| `subtitle` | string | recommended | Request card subtitle. |
| `actions` | table | recommended | Usually `{ 'accept', 'reject' }`. |
| `from` | table | recommended | Display sender context (`name`, `identifier`, `avatar`). |

### Apply bridge fields (critical)

| Field | Type | Required | Validation / Behavior |
|-------|------|----------|-----------------------|
| `requiresAccount` | bool | recommended | Canonical offer sets `false`; phone skips account picker for apply path. |
| `applyArgs.loanType` | string | yes (for real apply) | Must be valid key in `Config.LoanTypes`. |
| `applyArgs.termMonths` | number | yes (for real apply) | Must fit selected loan type bounds. |
| `applyArgs.bankId` | string | yes (for real apply) | Bank context for the loan application. |

### Issuer feedback fields

| Field | Type | Required | Behavior |
|-------|------|----------|----------|
| `issuerIdentifier` | string | recommended | Used for accept/reject/expire push notifications back to issuer. |
| `issuerName` | string | no | Used in notification/body labels and optional redirect transfer labels. |
| `bankId` | string | recommended | Used in preference-gated issuer notifications. |

### `destination` (optional payout redirect)

If provided and `amount > 0`, `loan_offer` accept tries to move funds from borrower primary to this destination after apply step.

| `destination.kind` | Required fields | Behavior |
|--------------------|-----------------|----------|
| `'identifier'` | `identifier` optional | If omitted, falls back to `payload.issuerIdentifier`. |
| `'account'` | `accountId` | Resolves account owner and transfers to that account. |
| `'society'` | `societyId` (number or name) | Debits borrower primary, credits society treasury. |

If destination is omitted, standard loan apply flow is used (no redirect transfer).

### `metadata` (display-only)

`metadata` is informational for request UI and does not enforce business rules directly.

## `opts` for `CreateRequest`

| Field | Type | Required | Behavior |
|-------|------|----------|----------|
| `fromIdentifier` | string | recommended | Sender identity stored on request row and used for sender-side updates. |
| `expiresInDays` | number | common | Common offer pattern is days-based expiry (often `3`). |
| `expiresInMinutes` | number | optional | Takes precedence over days when both are provided. |
| `accountId` | number | optional | Enables member fan-out push when request should notify a shared/business account circle. |

## Recommended Workflow

`OfferLoan` is **not mandatory**.

For vendor flows, recommended sequence is:

1. Call `GetAllBankingInfo(target)` and read `availableLoans`.
2. Pick a row where `canApply == true` (and usually `targetHasAccount == true`).
3. Choose `amount <= eligibleMax`, within `minAmount..maxAmount`, and a term within `minTermMonths..maxTermMonths`.
4. Create `loan_offer` via `CreateRequest(...)` using those values in `applyArgs`.

## What `OfferLoan` Actually Does

`OfferLoan` helper validates:

1. `loanType` exists
2. `amount` is inside loan type min/max
3. `termMonths` is inside loan type min/max
4. target identifier exists

It is a payload builder + basic guardrail helper, not the mandatory path.

## Examples

### 1) Recommended: precheck with `GetAllBankingInfo`, then `CreateRequest`

```lua
local info = exports['pc-banking']:GetAllBankingInfo({ targetIdentifier = targetIdentifier })
if not info or not info.success then return end

local chosen
for _, loan in ipairs(info.availableLoans or {}) do
    if loan.loanType == 'vehicle' and loan.bankId == 'maze' and loan.canApply then
        chosen = loan
        break
    end
end
if not chosen then return end

local amount = math.min(75000, chosen.eligibleMax or 0)
if amount < (chosen.minAmount or 0) then return end
local termMonths = math.max(chosen.minTermMonths or 1, 24)
termMonths = math.min(termMonths, chosen.maxTermMonths or termMonths)

local requestId = exports['pc-banking']:CreateRequest(targetIdentifier, 'loan_offer', {
    title = ('%s Offer'):format(chosen.label or 'Loan'),
    subtitle = 'Premium Motors',
    amount = amount,
    from = { name = 'Premium Motors', identifier = vendorIdentifier, avatar = 'PM' },
    actions = { 'accept', 'reject' },
    requiresAccount = false,
    applyArgs = {
        loanType = chosen.loanType,
        termMonths = termMonths,
        bankId = chosen.bankId,
    },
    metadata = {
        apr = ('%.1f%%'):format(chosen.interestRate or 0),
        term = ('%d mo'):format(termMonths),
        bank = chosen.bankLabel,
    },
    issuerIdentifier = vendorIdentifier,
    issuerName = 'Premium Motors',
    bankId = chosen.bankId,
}, {
    fromIdentifier = vendorIdentifier,
    expiresInDays = 3,
})
```

### 2) Loan offer with payout redirect to society

```lua
local requestId = exports['pc-banking']:CreateRequest(targetIdentifier, 'loan_offer', {
    title = 'Business Credit Line',
    subtitle = 'Maze Commercial',
    amount = 200000,
    from = { name = 'Maze Commercial', identifier = issuerIdentifier, avatar = 'MC' },
    actions = { 'accept', 'reject' },
    requiresAccount = false,
    applyArgs = {
        loanType = 'business',
        termMonths = 36,
        bankId = 'maze',
    },
    destination = { kind = 'society', societyId = 12 },
    issuerIdentifier = issuerIdentifier,
    issuerName = 'Maze Commercial',
    bankId = 'maze',
}, {
    fromIdentifier = issuerIdentifier,
    expiresInDays = 5,
})
```

### 3) Loan offer with payout redirect to specific account

```lua
local requestId = exports['pc-banking']:CreateRequest(targetIdentifier, 'loan_offer', {
    title = 'Bridge Loan',
    subtitle = 'Pacific Standard',
    amount = 150000,
    from = { name = 'Pacific Standard', identifier = issuerIdentifier, avatar = 'PS' },
    actions = { 'accept', 'reject' },
    requiresAccount = false,
    applyArgs = {
        loanType = 'property',
        termMonths = 48,
        bankId = 'pacific',
    },
    destination = { kind = 'account', accountId = 4421 },
    issuerIdentifier = issuerIdentifier,
    issuerName = 'Pacific Standard',
    bankId = 'pacific',
}, {
    fromIdentifier = issuerIdentifier,
    expiresInDays = 2,
})
```

### 4) Optional helper path: `OfferLoan` (not mandatory)

```lua
local res = exports['pc-banking']:OfferLoan(targetIdentifier, {
    loanType = 'vehicle',
    amount = 75000,
    termMonths = 24,
    bankId = 'maze',
    issuerIdentifier = vendorIdentifier,
    issuerName = 'Premium Motors',
    expiresInDays = 3,
})
```
