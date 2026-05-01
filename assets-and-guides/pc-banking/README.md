# PC-Banking

{% hint style="info" %}
Full-stack banking resource for FiveM. Multi-bank, multi-account, with cards, loans, savings, standing orders, shared/business accounts, phone integration, and a unified request system.
{% endhint %}

## Description

PC-Banking is a complete banking system for QBCore, Qbox, and ESX servers. It replaces stock framework money handling with a multi-bank infrastructure where players hold accounts at three banks (Fleeca, Maze, Pacific Standard), each with their own account types, card products, and loan offerings.

The resource ships with a desktop banking UI, a phone-app companion (`pc-banking-phone`), backwards-compatibility shims for `qb-banking` / `qb-management` / `Renewed-Banking` / `esx_addonaccount` / `okokBanking`, and a developer-facing exports surface for vendor scripts.

## Features

* Multi-bank: Fleeca, Maze Bank, Pacific Standard, each with their own brand, IBAN prefix, account/card/loan availability
* Account types: checking, savings, shared, business — with member roles and per-account permissions
* Cards: debit + credit, with daily/monthly limits, PIN, lock/unlock, and physical card items
* Loans: bank-scoped or global exposure, credit score, EMI scheduler, collateral, default lifecycle, write-off
* Savings: goal-based, interest accrual, deposit/withdrawal limits, term locks
* Standing orders: scheduled recurring transfers (P2P, society, vendor)
* Bills system: vendor-billed payments via the request system
* Society / business accounts with payroll, member roles, deposit/withdraw permissions
* Shared accounts with co-members (full / deposit-only / view permissions)
* Account freezing (admin or court order)
* Two-factor authentication for high-value transfers, password changes, card management
* Phone integration: `lb-phone`, `qs-smartphone`, `qb-phone`, `npwd`, `gksphone`, `17mov_Phone`
* Live push notifications to phone apps for transfers, bills, requests, EMIs
* Unified request system: loan offers, nearby transfers, direct payments, contact adds, member invites
* Cross-resource exports for vendor scripts: `CreateRequest`, `GetAllBankingInfo`, `OfferLoan`
* Backwards-compatibility shims for legacy banking resources
* 10 locales: en, es, fr, de, it, pt, sv, ja, cn, ar

## Guides

* [Installation](installation.md)
* [Banking Guide](guide/README.md)
* [Configuration](configuration/README.md)
* [Exports](exports/README.md)
