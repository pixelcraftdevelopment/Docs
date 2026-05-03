# Servicing & Maintenance

## Servicing System Overview

**How the servicing system works:**

- **Degradation Levels:** Each component has degradation 0-100%
- **Usage-Based:** Degradation increases with mileage and usage
- **Per-Vehicle Tracking:** Data saved per vehicle plate
- **Owner-Specific:** New owners get fresh servicing data

**Viewing and managing servicing parts:**

1. Connect to vehicle and navigate to "Servicing" app in tablet
2. View degradation levels for each component
3. Identify critical components (red/high degradation)
4. Obtain required servicing items from shop/stash
5. Use servicing items on vehicle to replace degraded parts
6. Component degradation resets to 0% after replacement

**Common serviceable components:**

- Engine Oil & Filter
- Brake Pads & Rotors
- Tires & Alignment
- Battery & Electrical
- Suspension Components
- Transmission Fluid

![Servicing System Overview](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/MechanicGuide/images/Servicing/1.png)

![Component Servicing](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/MechanicGuide/images/Servicing/2.png)

## Component Degradation Effects

**Each component affects vehicle performance differently:**

- **Suspension:** Reduces camber stiffness, suspension force, anti-roll bar force. Vehicle handles poorly.
- **Tyres:** Reduces traction curve min/max. Vehicle loses grip and slides.
- **Brake Pads:** Reduces brake force. Braking distance increases dramatically.
- **Clutch:** Reduces gear change rates. Slow, sluggish shifting.
- **Air Filter/Engine Oil:** Reduces acceleration and top speed. Engine audio degrades.
- **Spark Plugs:** Below 10%, random engine shutdowns occur. At 0%, permanent shutdown.

## Engine Seizure System

1. Engine oil degrades with use and damage
2. Below 10% oil: Engine temperature rises, occasional shutdowns
3. At 0% oil: If driven for configured time (30-90 sec), engine seizes
4. Seized engine: Complete shutdown, smoke effects, cannot start
5. **Fix:** TunePro app → Engines category → Engine Replacement
6. Prevent: Service oil regularly before reaching critical levels

![Engine Seizure Warning](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/MechanicGuide/images/Servicing/3.png)

![Engine Replacement in TunePro](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/MechanicGuide/images/Servicing/4.png)

## Oil Leak System

1. **Trigger:** Severe vehicle damage (moderate/severe crashes)
2. Oil leak particle effects appear under vehicle
3. Oil degrades: 3% per interval when engine running, 1.5% when off
4. Visual oil puddle trail left behind vehicle
5. **Fix:** Use welding torch item to seal the leak
6. Once fixed, oil stops leaking but still needs refilling

![Oil Leak Detection](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/MechanicGuide/images/Servicing/5.png)

![Welding Torch Repair](https://raw.githubusercontent.com/pixelcraftdevelopment/Guides/main/MechanicGuide/images/Servicing/6.png)

## Initial Servicing Data

1. New vehicles get initial servicing data from server
2. Based on vehicle ownership status
3. Saved to vehicle's statebag
4. Synchronized across all players
5. Persists between server restarts
