# Banking Commands

This page lists player-usable chat commands for `pc-banking`.

At the moment, there are no documented player chat commands available in the current scripts.

## Server Console / Admin Commands

### `pcbank_migrate`

Migrates legacy banking data into `pc-banking`.

Usage examples:

```text
pcbank_migrate
pcbank_migrate auto
pcbank_migrate qb
pcbank_migrate fd
pcbank_migrate qb ps okok
```

Supported source keys:

- `qb`
- `esx`
- `renewed`
- `okok`
- `ps`
- `omes`
- `qs`
- `tgg`
- `fd`

Notes:

- Console-only command.
- Requires ACE permission `command.pcbank_migrate`.

### `bankresetpassword`

Resets a player's banking login password. This is an administrator command and can be run from the server console or in-game chat by an ACE-authorized administrator.

```text
/bankresetpassword <id|name|account|card> <newPassword> <target...> [--bank=<bankId>]
```

| Argument | Description |
|----------|-------------|
| Lookup type | `id` resolves a character identifier, `name` resolves a character name, `account` resolves an account number, and `card` resolves a card number. |
| `newPassword` | New banking password. It must meet `Config.MinPasswordLength` and cannot exceed 128 characters. |
| Target | The identifier, character name, account number, or card number corresponding to the selected lookup type. Names containing spaces are supported. |
| `--bank=<bankId>` | Optional bank scope. For `id` and `name` lookups, omitting it resets every credentialed bank profile owned by that character. Account and card lookups are automatically scoped to their associated bank. |

Examples:

```text
/bankresetpassword id ABC123 NewPassword123
/bankresetpassword name "John Doe" NewPassword123 --bank=fleeca
/bankresetpassword account 1234-5678 NewPassword123
/bankresetpassword card 5555-5555-5555-5555 NewPassword123
```

Notes:

- Requires ACE permission `command.bankresetpassword`.
- The player is signed out of affected PC-Banking and phone-app sessions, then notified of the reset.
- The command fails if no banking login profile exists for the resolved character and bank scope.
