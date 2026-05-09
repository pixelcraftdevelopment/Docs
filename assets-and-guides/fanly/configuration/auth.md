# Session Tokens

Controls how long phone sign-in is remembered.

```lua
Config.Auth = {
    sessionDurationHours = 24,
}
```

## sessionDurationHours

How many hours a saved phone session stays valid before the player has to sign in again with username + password.

* Default `24` — once a player signs in, they can close and reopen the app for the next 24 hours without re-entering credentials.
* `0` — token never expires (session persists indefinitely until manually signed out).

## Tuning

* **Single-player households / RP servers** — raise to `168` (7 days) or `0` for fewer login prompts.
* **Shared-machine servers / public RP** — drop to `8` or lower so players can't accidentally leave their session open for the next person on the seat.

## Cross-Account Sign-In and Tokens

Tokens are issued **only** when the player signs in with their own character's credentials. If a player signs in with someone else's username + password (cross-account use), the session stays in memory only — no token is saved on the phone.

This means a leaked token can never silently resume a foreign account. The borrowed session ends the moment the app closes.

## Forgot Password

Independent of session length, the forgot-password flow sends a reset code over SMS to the **account owner's** phone (not the device requesting the reset). If the owner is offline at the time, the reset is blocked — they need to be in the city to receive the code.
