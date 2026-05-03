# Mechanic Jobs Whitelist

```lua
Config.MechanicJobs = { "mechanic" }
```

A flat list of framework job names that PC-Mechanic recognizes as mechanic jobs. Every owned shop's role mapping (`frameworkGrades` → internal role) only applies if the player's framework job is in this list.

## Why This Exists

Servers often run multiple mechanic-style jobs:

- `mechanic` (LS Customs)
- `tuner` (Benny's-style boutique)
- `lscustoms` (separate brand)

Adding all three means any of those jobs lets a player be on a mechanic role at an owned shop. It also lets `Config.UseTabletCommand` open the tablet for any of them.

## Interaction With Shop `job` Field

Each `Config.ShopLocations[shopId]` entry can carry its own `job` field (e.g. `job = "police"` for the police garage). That **overrides** `MechanicJobs` for that shop — the shop is gated to its own job, and the role hierarchy still applies on top.

So a shop with `job = "police"`:

- Only police can be employees at that shop
- Within police, the same role mapping applies based on police grades

A shop **without** an explicit `job` field defaults to anyone in `Config.MechanicJobs`.

## Self-Service Whitelist

Owned shops can also have a `selfServiceJobs` array — completely separate from `MechanicJobs`. This lists which jobs are allowed to self-service at the shop when the shop allows off-duty self-service. By default LS Customs ships with `selfServiceJobs = { "police", "ambulance" }` so emergency services can fix vehicles after-hours.

This is independent — a player on `selfServiceJobs` is **not** considered a shop employee. They just get the customization menu.
