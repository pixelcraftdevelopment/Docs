# Exports

Server-side exports exposed to other resources. All live under the `pc-banking` resource namespace, plus a few under `pc-banking-phone`.

**Side indicator:** `Server` means the export must be called from server-side Lua. No public client-side banking exports are currently exposed.

## pc-banking

### Money Management

* `Server` [AddMoney](AddMoney.md)
* `Server` [RemoveMoney](RemoveMoney.md)
* `Server` [GetBalance](GetBalance.md)
* `Server` [GetAvailableBalance](GetAvailableBalance.md)
* `Server` [GetOverdraftInfo](GetOverdraftInfo.md)

### Society / Business Treasury

* `Server` [AddSocietyMoney](AddSocietyMoney.md)
* `Server` [RemoveSocietyMoney](RemoveSocietyMoney.md)
* `Server` [GetSocietyBalance](GetSocietyBalance.md)
* `Server` [RegisterSociety](RegisterSociety.md)

### Account Freeze

* `Server` [FreezeAccount](FreezeAccount.md)
* `Server` [UnfreezeAccount](UnfreezeAccount.md)
* `Server` [IsAccountFrozen](IsAccountFrozen.md)

### Lookup (Read-Only)

* `Server` [GetAllBankingInfo](GetAllBankingInfo.md)
* `Server` [GetAccountInfo](GetAccountInfo.md)
* `Server` [GetAccountsByIdentifier](GetAccountsByIdentifier.md)
* `Server` [GetAccountFromCard](GetAccountFromCard.md)
* `Server` [IsCardFrozen](IsCardFrozen.md)
* `Server` [GetCreditInfoFromCard](GetCreditInfoFromCard.md)
* `Server` [ExportAccountTransactions](ExportAccountTransactions.md)

### Requests (Phone-App Inbox)

* `Server` [CreateRequest](CreateRequest.md)
* `Server` [CreateBill](CreateBill.md)

### Logging

* `Server` [LogTransaction](LogTransaction.md)

## pc-banking-phone

* `Server` [PushToApp](PushToApp.md)
* `Server` [PushToAppForIdentifier](PushToAppForIdentifier.md)
* `Server` [GetPhoneSessionIdentifier](GetPhoneSessionIdentifier.md)

## Internal / Admin Only

These exports exist but are gated to admin tooling, not for vendor scripts:

* `getAdminConfig`, `getAdminSocietyConfig`, `isAceAdminForSociety` — admin panel feeds
* `_pcAdminWriteConfig` — config hot-reload writer
* `OfferLoan` — internal wrapper used by the bundled billing scaffold; vendor scripts should use `CreateRequest('loan_offer', ...)` instead
* `ReportError` — error pipeline
