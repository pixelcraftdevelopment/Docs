# Payment Request (`direct_payment`)

Type key for `CreateRequest`: `direct_payment`

## Export Call

```lua
local requestId = exports['pc-banking']:CreateRequest(target, 'direct_payment', payload, opts)
```

## `target`

| Param | Type | Required | Notes |
|-------|------|----------|-------|
| `target` | string \| number | yes | Target identifier (string) or server source id (number). Number is resolved to identifier first. |

## `payload` Schema

`CreateRequest` does not hard-validate payload shape. Validation happens when the request is processed.

### Required for successful accept flow

| Field | Type | Required | Validation / Behavior |
|-------|------|----------|-----------------------|
| `amount` | number | yes | Must parse to number and be `> 0` on accept. |
| `destination` | table | yes | Must include valid `kind` (see destination section). |

### Source selection fields

| Field | Type | Required | Validation / Behavior |
|-------|------|----------|-----------------------|
| `sourceAccountId` | number | conditional | Optional pre-bound funding account. On accept, resolver-provided `sourceAccountId` takes precedence over this payload field. |
| `sourceCardId` | number | conditional | Optional pre-bound funding card. |
| `requiresAccount` | bool | no | UI hint. If `false`, the client can skip account picker. Processing still requires either account or card source at accept time. |

At accept time, if neither source account nor source card is available, request fails with no-source error.

### Display / metadata fields used in UX and logs

| Field | Type | Required | Used For |
|-------|------|----------|----------|
| `title` | string | no | Request list/toast title. |
| `subtitle` | string | no | Request list/toast subtitle. |
| `actions` | table | no | UI action labels (commonly `{ 'accept', 'reject' }`). |
| `merchantTag` | string | no | Vendor label shown to payer / used in transfer labels. |
| `from` | table | no | `from.name` is used as sender name fallback for transfer/log text. |
| `bankId` | string | no | Passed as sender bank id in transfer execution context. |
| `destLabel` | string | no | UI subtitle helper label for destination preview. |

## `destination` Object

```lua
destination = {
  kind = 'identifier' | 'account' | 'society',
  -- identifier mode
  identifier = 'char:abc123',
  -- account mode
  accountId = 42,
  -- society mode
  societyId = 7 -- or 'society_name'
}
```

### `kind = 'identifier'`

| Field | Type | Required | Behavior |
|-------|------|----------|----------|
| `identifier` | string | no | If omitted, system falls back to request sender identifier. |

### `kind = 'account'`

| Field | Type | Required | Behavior |
|-------|------|----------|----------|
| `accountId` | number | yes | Must map to a valid bank account; account owner becomes transfer recipient identifier. |

### `kind = 'society'`

| Field | Type | Required | Behavior |
|-------|------|----------|----------|
| `societyId` | number \| string | yes | Numeric society id or society name lookup. Funds are credited to society balance (not account transfer path). |

Any other `kind` value fails as invalid destination.

## `opts` for `CreateRequest`

| Field | Type | Required | Behavior |
|-------|------|----------|----------|
| `fromIdentifier` | string | recommended | Stored in request row; used for sender-side push updates and fallback destination logic. |
| `expiresInMinutes` | number | no | If `> 0`, sets `expires_at = now + minutes`. Takes priority over days. |
| `expiresInDays` | number | no | Used only when minutes is absent. |
| `accountId` | number | no | If provided, create-time push fan-outs to members of that shared/business account. |

## Canonical Producer Pattern (from code)

Recommended producer pattern:

1. `title`, `subtitle`, `amount`
2. `from = { name, identifier }`
3. `actions = { 'accept', 'reject' }`
4. `merchantTag`, `destination`, optional `sourceAccountId` / `sourceCardId`
5. `requiresAccount = (sourceAccountId == nil and sourceCardId == nil)`

Using this shape keeps phone UX and accept flow aligned with current runtime.

## Examples

### 1) Minimal payment request (identifier destination, payer picks source)

```lua
local requestId = exports['pc-banking']:CreateRequest(customerSrc, 'direct_payment', {
    title = 'Payment Request',
    subtitle = 'Pay to mechanic',
    amount = 2500,
    destination = { kind = 'identifier', identifier = vendorIdentifier },
    from = { name = 'Bennys', identifier = vendorIdentifier },
    actions = { 'accept', 'reject' },
    requiresAccount = true,
}, {
    fromIdentifier = vendorIdentifier,
    expiresInMinutes = 15,
})
```

### 2) Pre-bound account source (skip picker)

```lua
local requestId = exports['pc-banking']:CreateRequest(customerIdentifier, 'direct_payment', {
    title = 'Invoice #204',
    subtitle = 'City Services',
    amount = 1200,
    destination = { kind = 'identifier', identifier = cityTreasuryIdentifier },
    sourceAccountId = 1832,
    requiresAccount = false,
    from = { name = 'City Services', identifier = cityTreasuryIdentifier },
    actions = { 'accept', 'reject' },
}, {
    fromIdentifier = cityTreasuryIdentifier,
    expiresInMinutes = 10,
})
```

### 3) Society destination

```lua
local requestId = exports['pc-banking']:CreateRequest(customerSrc, 'direct_payment', {
    title = 'Tow Charge',
    subtitle = 'Deposit to society',
    amount = 3000,
    destination = { kind = 'society', societyId = 7 }, -- numeric id or society name
    from = { name = 'Impound', identifier = impoundIdentifier },
    merchantTag = 'IMPOUND',
    actions = { 'accept', 'reject' },
}, {
    fromIdentifier = impoundIdentifier,
    expiresInMinutes = 20,
})
```

### 4) Account destination

```lua
local requestId = exports['pc-banking']:CreateRequest(customerIdentifier, 'direct_payment', {
    title = 'Private Invoice',
    subtitle = 'Transfer to specific account',
    amount = 1800,
    destination = { kind = 'account', accountId = 4421 },
    from = { name = 'Vendor A', identifier = vendorIdentifier },
    actions = { 'accept', 'reject' },
    requiresAccount = true,
}, {
    fromIdentifier = vendorIdentifier,
    expiresInDays = 1,
})
```
