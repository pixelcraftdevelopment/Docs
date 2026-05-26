# RegisterSociety

**Side:** Server

Create a new society at runtime. Idempotent — does nothing if a society with the same name already exists.

```lua
local created = exports['pc-banking']:RegisterSociety(jobName, opts)
```

| Param | Type | Notes |
|-------|------|-------|
| `jobName` | string | Job key (must match framework job name for auto-link) |
| `opts.type` | string | `'business'` (default) or `'civilian'` |
| `opts.owner` | string | Owner identifier (default `'system'`) |

## Returns

* `true` if newly created
* `false` if already exists or invalid input

## Side Effects

Inserts a row into `pc_banking_societies` with `balance = 0`, `job_locked = 1`, and `members = '[]'`.

## Examples

```lua
exports['pc-banking']:RegisterSociety('newcompany', {
    type  = 'business',
    owner = ownerIdentifier,
})

-- Civilian fund (not job-locked use case)
exports['pc-banking']:RegisterSociety('cityrelief', { type = 'civilian' })
```
