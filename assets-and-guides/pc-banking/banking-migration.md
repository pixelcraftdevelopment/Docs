# Migration

`pc-banking` ships with one-shot importers for the most common FiveM banking scripts and base frameworks. Run from the **server console**:

```
pcbank_migrate auto
```

…or target a single source:

```
pcbank_migrate qb | esx | renewed | okok | ps | omes | qs | tgg | fd
```

You can chain multiple sources in a single call (e.g. `pcbank_migrate qb okok` will import player accounts from QB and societies/loans from okokBanking).

`auto` mode runs every migrator in detection order and silently skips ones whose source tables aren't present, so it's safe to run on any setup. **Run on a fresh / empty pc-banking database** — re-running the same migrator will skip rows that already exist (`INSERT IGNORE`), but the safest path is one-shot import on first install.

---

## What each migrator handles

Legend: ✅ imported · ❌ no equivalent / not migrated · ⚠️ partial

| Source | Accounts | Societies | Members | Transactions | Cards | Loans | Savings |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **QB-Core / Qbox** (`qb`) | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **ESX** (`esx`) | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Renewed Banking** (`renewed`) | ✅ | ✅ | ⚠️ | ✅ | ❌ | ❌ | ❌ |
| **okokBankingv2** (`okok`) | ✅ | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ |
| **ps-banking** (`ps`) | ❌ | ✅ | ⚠️ | ✅ | ❌ | ❌ | ❌ |
| **omes_banking** (`omes`) | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ✅ |
| **qs-banking** (`qs`) | ❌ | ✅ | ⚠️ | ✅ | ✅ | ❌ | ❌ |
| **tgg-banking** (`tgg`) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| **fd_banking** (`fd`) | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ |

> ⚠️ in **Members** = members embedded in `JSON` on the legacy society/account row, copied as a JSON list onto the pc-banking society. They aren't created as proper account-members with permission ENUMs (only `tgg` and `fd` do that).

---

## Source-table reference

What each migrator reads from your existing database.

| Source | Tables read |
|---|---|
| `qb` | `players` (`citizenid`, `money` JSON) |
| `esx` | `users` (`identifier`, `accounts` JSON) |
| `renewed` | `bank_accounts_new`, `player_transactions` |
| `okok` | `okokbanking_accounts`, `okokbanking_societies`, `okokbanking_loans` |
| `ps` | `ps_banking_accounts`, `ps_banking_transactions` |
| `omes` | `banking_transactions`, `banking_savings` |
| `qs` | `bank_cards`, `bank_history`, `bank_statements`, `bank_accounts` |
| `tgg` | `tgg_banking_accounts`, `tgg_banking_account_members`, `tgg_banking_cards`, `tgg_banking_transactions`, `tgg_banking_loans` |
| `fd` | `fd_advanced_banking_accounts`, `fd_advanced_banking_accounts_members`, `fd_advanced_banking_accounts_transactions` |

---

## Auto-detection order

When you run `pcbank_migrate auto` (or no argument), migrators fire in this order. **Specific banking scripts run before base frameworks** so we don't double-create the bank account from `players`/`users` when a richer source is already present:

```
tgg → fd → renewed → okok → ps → omes → qs → qb → esx
```

If the tables for a given source aren't present, that migrator prints a `Skipped (...)` line and moves on.

---

## Notes & caveats

- **Default bank / account type** for every imported account comes from `Config.DefaultBank` and that bank's `defaultCheckingType`. Savings imports (omes) need at least one `savings_*` entry in `availableAccountTypes`.
- **Account numbers** — for legacy sources without IBAN-style numbers (qb, esx, renewed, omes), pc-banking generates fresh `MGxxxxxxxxxxxx` numbers. okok, qs, tgg, fd preserve the source IBAN/card numbers.
- **Primary / default flag** — the first imported account per owner is marked `is_primary = is_default = 1`. Subsequent accounts (multi-bank, savings) come in as non-primary.
- **Transactions** — `INSERT IGNORE` is **not** used (we want history). Re-running a transaction migrator can duplicate rows. Run once.
- **`tgg-banking`** skips `closed = 1` accounts and `terminated = 1` cards. The skip count is printed at the end.
- **`fd_banking`** skips invoices/tracking tables — pc-banking has no equivalent for those flows.
- **`ps-banking`** stores all accounts as shared/org rows, so they all map to **societies** in pc-banking (no personal accounts created).
- **`qs-banking`** requires at least one of `bank_cards`, `bank_history`, `bank_statements` — `bank_accounts` alone is ambiguous (qb-banking also uses that name) so it's rejected on its own.
- **Permission mapping** — `tgg` and `fd` member permissions collapse to pc-banking's `view | deposit | full | admin` ENUM:
  - `is_owner` / `can_control_members` → `admin`
  - `can_withdraw` / `can_transfer` → `full`
  - `can_deposit` only → `deposit`
  - everything else → `view`

---

## After migration

Verify the totals printed at the end of the run:

```
Migration complete!
  Accounts:     N
  Societies:    N
  Transactions: N
  Cards:        N
  Loans:        N
  Savings:      N
```

Hop into the in-game banking UI as a player whose data was imported and confirm balance, account list, and transaction history match your old script. If something looks off, [report it on Discord](https://discord.gg/2bfZKaHtN9) with the migrator name + your previous script's version.
