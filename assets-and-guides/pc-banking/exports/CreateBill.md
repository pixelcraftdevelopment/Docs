# CreateBill

**Side:** Server

Creates a native PC-Banking bill request for a player.

```lua
local result = exports['pc-banking']:CreateBill(target, data)
```

| Param | Type | Notes |
|-------|------|-------|
| `target` | string \| number | Recipient identifier or server source. |
| `data` | table | Bill configuration. |

```lua
local result = exports['pc-banking']:CreateBill(playerSrc, {
    title = 'Vehicle repair',
    amount = 2500,
    destination = { kind = 'society', societyId = 'mechanic' },
    dueIn = '7D',
    autoPay = true,
    affectsCredit = true,
})
```

`data.destination` must be one of:

* `{ kind = 'account', accountId = number }`
* `{ kind = 'identifier', identifier = string }`
* `{ kind = 'society', societyId = number|string }`

Optional fields are `description`, `issuer`, `fromIdentifier`, `accountId`, and `freezeAfter`. `dueIn` is required; `freezeAfter` can be `false` to disable post-due account freezing.

## `data` flags

| Field | Type | Behavior |
|-------|------|----------|
| `title` | string | Bill title shown to the recipient. Defaults to the localized bill title. |
| `amount` | number | Required positive whole-number amount. |
| `destination` | table | Required payout destination, using one of the shapes above. |
| `dueIn` | string | Required interval until the bill becomes due, for example `'30S'`, `'1D'`, or `'7D'`. |
| `autoPay` | boolean | When `true`, the bill scheduler attempts to pay the bill at/after its due time. Failed attempts leave the bill pending. |
| `affectsCredit` | boolean | When `true`, unresolved or paid-late bills participate in the existing credit-score consequence calculation. |
| `freezeAfter` | string \| false | Interval after the due time before the bill's source account is frozen. Set `false` or omit it to disable freezing. |
| `accountId` | number | Optional source account. The target must have full access to it; otherwise the recipient selects a payment account. |
| `description` | string | Optional body text shown with the bill. |
| `issuer` | string | Optional issuer name. Defaults to the calling resource or `System`. |
| `fromIdentifier` | string | Optional issuer identifier retained with the bill record. |

## Return flags

| Field | Meaning |
|-------|---------|
| `success` | `true` when the bill was created. |
| `billId` | New PC-Banking request ID. |
| `dueAt` | Unix timestamp for the due time. |
| `freezeAt` | Unix timestamp at which a still-unpaid bill may freeze its source account, or `nil` when freezing is disabled. |
| `error` | `true` when validation or creation fails. |
| `message` | Localized failure reason when `error` is `true`. |
