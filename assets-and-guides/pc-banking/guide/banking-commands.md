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
