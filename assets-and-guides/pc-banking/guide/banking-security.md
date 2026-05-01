# Login & 2FA

## Banking Password

If banking-password login is enabled, the first time you open the UI you register a password (minimum 4 characters by default). On later opens you log in with that password.

Tick "remember me" to keep the session alive for 24 hours; otherwise it ends when you log out or restart. Server owners can disable password login entirely if they prefer no friction.

![Login screen](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/Security/1.png)

## Two-Factor Authentication

2FA adds a one-time code (delivered by SMS to the in-game phone) for sensitive actions:

- Transfers above the high-value threshold (default $10,000).
- Society payroll and admin payouts above the society threshold (default $25,000).
- Password changes and card management - always, regardless of amount.

OTP codes expire after 5 minutes, with a cooldown between requests and a max-attempts cap to block brute force.

![2FA OTP prompt](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/Security/2.png)

## Security Alerts

SMS / push alerts can fire for transfers, large transactions, security events (password changes, failed logins), and EMI debits. Each category has its own toggle in the config so server owners can pick which alerts ship.

