# PC-Mechanic

{% hint style="info" %}
Full-stack mechanic resource for FiveM. Vehicle servicing, damage-driven part wear, inspection minigames, tuning with custom handling data, dyno testing, mod menu, nitrous, role-based shop management, and a tablet workflow for on-duty mechanics.
{% endhint %}

## Description

PC-Mechanic is a complete vehicle workshop system for QBCore, Qbox, and ESX servers. It pairs a player-facing customization UI (mods, paint, wheels, stance) with a deep maintenance layer where parts wear over time and damage, vehicles fail when neglected, and mechanics fix them through inspection and replacement workflows.

The resource ships with self-service shops (Benny's-style walk-up tuning), owned shops (mechanic-managed with employee tablets, repair zones, parts shops, and dyno stations), a mileage HUD, an oil-leak system with engine-seizure consequences, electric-vehicle support, and 13 locales.

## Features

* **Customization** — body kits, wheels, livery, paint (Metallic, Matte, Util, Worn, Misc, Chameleon), neon lights, headlights, tyre smoke, bulletproof tyres, plate index, window tint, horn, extras
* **Stance** — adjustable suspension height, camber, and track width within configurable clamps
* **Tuning** — engines, drivetrains (AWD/RWD/FWD), tyres (slick/semi-slick/offroad), brakes, drift kits, anti-roll bars, launch control, with custom handling data per option
* **Mileage HUD** — km or miles, configurable display position and scale, accumulation multiplier, auto-purge for non-owned cars
* **Servicing** — suspension, tyres, brake pads, engine oil, clutch, air filter, spark plugs, EV motor, EV battery, EV coolant, each with its own item, durability, and degradation
* **Damage-driven wear** — parts degrade from body damage, engine damage, tyre bursts, and rollovers, scaled by hit severity
* **Engine consequences** — oil leaks on damage, low-oil engine shutdowns, complete engine seizure at 0% oil
* **Inspection minigames** — OBD diagnostics, tread test, pressure test, multimeter, dyno inspection, with item-gated tools and per-tool variants and difficulty
* **Electric vehicles** — auto-detected on game build 3258+, manual list for older builds, EV-only parts and tuning
* **Dyno** — alignment overlay, DUI screen, per-plate test history
* **Nitrous** — bottle inventory, partial refills, purging drain, configurable boost duration and cooldown
* **Mod menu** — performance, cosmetics, stance, respray, wheels, neon, headlights, tyre smoke, bulletproof tyres, extras
* **Shops** — self-service or owned, with per-shop mod/tuning toggles, repair zones, walk-up parts shops, stashes, dyno stations
* **Roles** — owner / manager / mechanic / novice with granular permissions, framework-grade mapping, server admin override
* **Repair zones** — polygon enforcement with auto-snap, ceiling detection, in-MLO support, and visual flash on violation
* **Tablet** — on-duty workflow for orders, invoices, analytics, and management
* **Pricing engine** — vehicle-value scaled, profit-margin or buffer modes, lowest/highest shop price selection
* **Discord webhooks** — work orders, servicing, billing, staff management
* **13 locales** — en, ar, cn, de, es, fr, hu, it, ja, pt, sv, zh-tw

## Guides

* [Installation](installation.md)
* [Mechanic Guide](guide/README.md)
* [Configuration](configuration/README.md)
* [Events](events/README.md)
* [Exports](exports/README.md)
