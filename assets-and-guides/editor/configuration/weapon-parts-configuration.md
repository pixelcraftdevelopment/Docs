# Weapon Parts Configuration

{% hint style="info" %}
Adding custom parts is not supported, do not add any new parts to Config.Parts
{% endhint %}

* **Purpose:** Defines the parts that make up each weapon and their individual damage frequencies.
*   **Structure:**

    ```
    ["weapon_pistol"] = { --WeaponName
        ["barrel"] = { damageFrequency = 0.85 }, --Damage frequency of each part on fire
        ["front_sight"] = { damageFrequency = 0.6 },
        ["hammer"] = { damageFrequency = 1.1 },
        ["magazine"] = { damageFrequency = 0.4 },
        ["rear_sight"] = { damageFrequency = 0.5 },
        ["recoil_spring_guide"] = { damageFrequency = 1.2 },
        ["slide"] = { damageFrequency = 0.5 },
        ["trigger"] = { damageFrequency = 1.05 }
    },
    ```
* **Damage Frequency:** Represents how much damage a part takes relative to the overall weapon damage. A higher value means the part degrades faster.
