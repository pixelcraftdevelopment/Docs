# Societies & Payroll

## Society Types

Society accounts back jobs and player organisations. Two flavours:

- **Job-locked societies** - Police, EMS, Mechanic. Created automatically from your framework's job list. Members are added/removed when their job changes.
- **Player-created societies** - Gangs, Businesses, Government orgs. Founded by a player and grown by inviting members.

Server owners can add new job-locked societies by editing the society config and restarting; the script picks them up automatically.

## Roles & Grades

Job-locked societies use the framework's grade levels (0 to 4 by default), each with its own withdraw permission, withdraw cap, and management rights. Player-created societies use named roles - Owner, Manager, Employee - that the founder can rename and tweak.

![Society dashboard](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/Societies/1.png)

## Running Payroll

Bosses (or admins with the right ACE permission) can run payroll from the society dashboard:

- **One-shot payroll** - credit a fixed amount to every active member right now.
- **Scheduled payroll** - set a per-grade salary that pays automatically on a recurring cadence.
- Each run is logged and shows up in the society's audit history.

![Payroll](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/BankingGuide/images/Societies/2.png)

