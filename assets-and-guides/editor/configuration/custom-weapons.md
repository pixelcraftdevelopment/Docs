# Custom Weapons



{% embed url="https://youtu.be/1FxN5rH55bE" %}

* **Purpose:** Connects your custom weapon names to the available weapon models in the script
* Make the custom weapon parts entry same as the weapon you are mapping it to:&#x20;
  * ```
    Say, if you're mapping your custom weapon to weapon_pistol.glb: 
        ["weapon_pistol"] = {
            ["front_sight"] = { damageFrequency = 0.60 },
            ["recoil_spring_guide"] = { damageFrequency = 1.20 },
            ["hammer"] = { damageFrequency = 1.10 },
            ["rear_sight"] = { damageFrequency = 0.50 },
            ["barrel"] = { damageFrequency = 0.85 },
            ["slide"] = { damageFrequency = 0.50 },
            ["magazine"] = { damageFrequency = 0.40 },
            ["trigger"] = { damageFrequency = 1.05 },
        },
    You're entry for your custom weapon will be: 
        ["weapon_custom"] = {
            ["front_sight"] = { damageFrequency = 0.60 },
            ["recoil_spring_guide"] = { damageFrequency = 1.20 },
            ["hammer"] = { damageFrequency = 1.10 },
            ["rear_sight"] = { damageFrequency = 0.50 },
            ["barrel"] = { damageFrequency = 0.85 },
            ["slide"] = { damageFrequency = 0.50 },
            ["magazine"] = { damageFrequency = 0.40 },
            ["trigger"] = { damageFrequency = 1.05 },
        },
    ```
*   **Structure:**

    ```
    weaponModelMap = {
        -- Standard weapons
        WEAPON_PISTOL = 'weapon_pistol.glb',
        weapon_carbinerifle = 'weapon_carbinerifle.glb',
        
        -- Custom weapons using standard models
        weapon_custom = 'weapon_pistol.glb',
    ```

{% hint style="info" %}
Adding custom parts is not supported, do not add any new parts to Config.Parts
{% endhint %}

