# Configuration

PC-Banking config is split across files in `pc-banking/config/`:

| File | Contains |
|------|----------|
| `config.lua` | Framework, locale, currency, notifications, phone, global limits, 2FA, scheduled tasks |
| `banks.lua` | Bank brands and which account/card/loan types each offers |
| `accounts.lua` | Account type definitions (checking/savings/shared/business) |
| `cards.lua` | Card type definitions and visual styles |
| `loans.lua` | Loan products, credit score formula, exposure scopes |
| `society.lua` | Society roles, grade permission defaults, type templates |
| `locations.lua` | Bank branch points, ATM models/services, inter-bank ATM fees |

Plus `pc-banking-phone/config.lua` for the phone companion.

## Sub-Pages

### Core

* [Framework, Locale, Currency](framework.md)
* [Banks](banks.md)
* [Account Types](account-types.md)
* [Card Types](card-types.md)
* [Loan Types](loan-types.md)
* [Society Configuration](society.md)
* [Locations and ATMs](locations.md)

### Limits and Auth

* [Global Limits](global-limits.md)
* [Two-Factor Authentication](two-factor.md)
* [Banking Password / Login](banking-password.md)

### Behavior

* [Card Overlay](card-overlay.md)
* [Fees](fees.md)
* [Auto-Payments](auto-payments.md)
* [Standing Orders](standing-orders.md)
* [Scheduled Tasks and Intervals](scheduled-tasks.md)

### Integrations

* [Phone Integration](phone-integration.md)
* [Discord Webhooks](webhooks.md)
* [Backwards Compatibility Shims](backwards-compat.md)

### Admin

* [Account Freezing](account-freezing.md)
* [Admin Tools (LEA + Server ACE)](admin.md)

### Phone Companion

* [pc-banking-phone Config](phone-config.md)
