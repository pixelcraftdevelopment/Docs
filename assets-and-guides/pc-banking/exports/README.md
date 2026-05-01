# Exports

Server-side exports exposed to other resources. All live under the `pc-banking` resource namespace, plus a few under `pc-banking-phone`.

## pc-banking

### Money Management

* [AddMoney](AddMoney.md)
* [RemoveMoney](RemoveMoney.md)
* [GetBalance](GetBalance.md)

### Society / Business Treasury

* [AddSocietyMoney](AddSocietyMoney.md)
* [RemoveSocietyMoney](RemoveSocietyMoney.md)
* [GetSocietyBalance](GetSocietyBalance.md)
* [RegisterSociety](RegisterSociety.md)

### Account Freeze

* [FreezeAccount](FreezeAccount.md)
* [UnfreezeAccount](UnfreezeAccount.md)
* [IsAccountFrozen](IsAccountFrozen.md)

### Lookup (Read-Only)

* [GetAllBankingInfo](GetAllBankingInfo.md)
* [GetAccountInfo](GetAccountInfo.md)
* [GetAccountsByIdentifier](GetAccountsByIdentifier.md)
* [GetAccountFromCard](GetAccountFromCard.md)
* [IsCardFrozen](IsCardFrozen.md)
* [GetCreditInfoFromCard](GetCreditInfoFromCard.md)
* [ExportAccountTransactions](ExportAccountTransactions.md)

### Requests (Phone-App Inbox)

* [CreateRequest](CreateRequest.md)

### Logging

* [LogTransaction](LogTransaction.md)

## pc-banking-phone

* [PushToApp](PushToApp.md)
* [PushToAppForIdentifier](PushToAppForIdentifier.md)
* [GetPhoneSessionIdentifier](GetPhoneSessionIdentifier.md)

## Internal / Admin Only

These exports exist but are gated to admin tooling, not for vendor scripts:

* `getAdminConfig`, `getAdminSocietyConfig`, `isAceAdminForSociety` — admin panel feeds
* `_pcAdminWriteConfig` — config hot-reload writer
* `OfferLoan` — internal wrapper used by the bundled billing scaffold; vendor scripts should use `CreateRequest('loan_offer', ...)` instead
* `ReportError` — error pipeline
