# Weapon Damage Multipliers

* **Purpose:** Controls the rate at which weapons degrade with each shot. Adjust these values according to the values in your server.
* **Adjusting Values:** Higher values lead to faster weapon degradation.
*   **Example:**

    ```
    Config.WeaponDamageMultiplier = {
        ["weapon_pistol50"] = 0.15, -- Degrades by 0.15 per shot
        ["weapon_pistol"] = 0.10,   -- Degrades by 0.10 per shot
        -- Add more weapons as needed
    }
    ```
