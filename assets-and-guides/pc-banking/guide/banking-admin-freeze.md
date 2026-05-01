# Admin Tools & Account Freezing

## Freezing Accounts (Law Enforcement)

Players in the configured law-enforcement jobs (police, FBI by default) above a minimum grade can freeze and unfreeze suspect accounts during investigations. A reason is required; both the affected player and admins are notified.

A frozen account can still be viewed but cannot send transfers, run standing orders, or approve card spends. Shared and business accounts can also be frozen.

![Admin freeze panel](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/Admin/1.png)

## Reverting Transactions

LEA can roll back paired transfers within a 7-day window (configurable). Single-sided entries - fees, cash deposits, interest, loan payments - cannot be reverted, since there is no counter-side to flip.

Every revert requires a reason and is logged. Both parties are notified that a transaction was reversed.

![Transaction revert](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/Admin/2.png)

## Society Oversight (Server Admin)

Separate from LEA tools, server admins with the right ACE permission can monitor and edit any society - adjust balances, run admin payrolls, add or remove members, change roles. This bypasses in-game job gating, so it's gated behind add_ace in server.cfg rather than a job check.

Affected members and the society owner are notified whenever an admin action runs.

![Society admin panel](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/Admin/3.png)

