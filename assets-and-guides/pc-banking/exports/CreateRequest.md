# CreateRequest

**Side:** Server

Create a request row in the target player's request inbox.

```lua
local requestId = exports['pc-banking']:CreateRequest(target, typeKey, payload, opts)
```

## Signature

| Param | Type | Required | Notes |
|-------|------|----------|-------|
| `target` | string \| number | yes | Identifier string or server source id. Source ids are resolved to identifier. |
| `typeKey` | string | yes | Request type key. For this docs set, use `direct_payment` or `loan_offer`. |
| `payload` | table | yes | Type-specific payload. No strict shape validation happens in this export itself. |
| `opts` | table | no | `{ fromIdentifier?, expiresInDays?, expiresInMinutes?, accountId? }` |

## Returns

1. `number` -> created request id
2. `nil` -> invalid target or create failure

## `opts` Fields

| Field | Type | Behavior |
|-------|------|----------|
| `fromIdentifier` | string | Stored as request sender identity; used by sender-side updates/notifications. |
| `expiresInMinutes` | number | If `> 0`, sets expiration timestamp. Takes precedence over days. |
| `expiresInDays` | number | Used when minutes is not set. |
| `accountId` | number | If provided, create-time push can fan out to members of shared/business account. |

If neither `expiresInMinutes` nor `expiresInDays` is provided, request does not auto-expire.

## Detailed Request Payload Docs

1. Payment request (`direct_payment`): [payment-request.md](../requests/payment-request.md)
2. Loan request (`loan_offer`): [loan-request.md](../requests/loan-request.md)
3. Requests index: [README.md](../requests/README.md)

## Important Behavior

`CreateRequest` is a transport/storage API. Type-level business validation happens when each request type is processed, and can also be done by upstream helper exports.

For loan offers, preferred vendor flow is: call `GetAllBankingInfo(target)` first, select an eligible row from `availableLoans` (`canApply`, `eligibleMax`, term bounds), then create `loan_offer` with `CreateRequest`.
