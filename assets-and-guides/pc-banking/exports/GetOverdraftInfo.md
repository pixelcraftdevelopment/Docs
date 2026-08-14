# GetOverdraftInfo

**Side:** Server

Returns an account's overdraft status and available balance.

```lua
local info = exports['pc-banking']:GetOverdraftInfo(accountId, channel)
```

| Param | Type | Notes |
|-------|------|-------|
| `accountId` | number \| table | Account ID, or a complete account record. |
| `channel` | string | Optional debit channel to evaluate, such as `transfer`, `withdrawal`, or `atm`. When omitted, the returned policy is evaluated for `transfer`. |

Returns `nil` when the account cannot be found. Otherwise returns:

| Field | Description |
|-------|-------------|
| `overdraftEnabled` | `true` when the account and selected channel are eligible for overdraft. |
| `overdraftLimit` | Eligible overdraft amount after global, account-type, and framework limits are applied. |
| `availableBalance` | Current balance plus eligible overdraft, never below zero. |
| `isOverdrawn` | `true` when the raw ledger balance is below zero. |
