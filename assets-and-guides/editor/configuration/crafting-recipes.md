# Crafting Recipes

* **Recipe Variables** (craftingrecipes.lua)

`name -- Internal name matching inventory system`&#x20;

`label -- Display name in UI`&#x20;

`threeD -- 3D model display (false for custom weapons)`&#x20;

`requiredXp -- XP needed to unlock`&#x20;

`rewardXP -- XP gained from crafting`&#x20;

`craftDuration -- Crafting time in milliseconds`&#x20;

`repairDuration -- Repair time in milliseconds (weapons only)`&#x20;

`description -- Item description`

&#x20;`heading -- Model rotation`&#x20;

`proximity -- Required distance of model from camera`&#x20;

`model -- Prop model`&#x20;

`image -- UI image`&#x20;

`requiredMaterials -- Crafting materials array`&#x20;

`requiredRepairMaterials -- Repair materials array (weapons)`

`quantity -- quantity of item to give at once`&#x20;

*   **Recipe Types:**

    * **Standard Items**

    <pre><code>['repairkit'] = {
        name = "repairkit",
        label = "Repair Kit",
        threeD = false,
        requiredXp = 10,
        rewardXP = 5,
        craftDuration = 15000,
        description = "Vehicle repair kit",
        model = 'prop_toolchest_01',
        image = 'repairkit.png',
        quantity = 2,
        requiredMaterials = {
    <strong>        {name = "metalscrap", label = 'Metal scrap', amount = 1},
    </strong>        {name = "steel", label = 'Steel', amount = 2}
        }
    }
    </code></pre>

    * **Weapons**

    ```
    ['weapon_pistol'] = {
        name = "weapon_pistol",
        label = "Pistol",
        threeD = true,
        requiredXp = 0,
        rewardXP = 10,
        craftDuration = 120000,
        repairDuration = 15000,
        description = "Standard pistol",
        image = 'weapon_pistol.png',
        requiredMaterials = {
            {name = "barrel", label = 'Barrel', amount = 1},
        },
    }
    ```

    *   **Custom Weapons or Weapons without 3d crafting**(Do not use this format if you're using weaponmodelmap to map your custom weapons)

        ```
        ['weapon_custom'] = {
            name = "weapon_custom",
            label = "Custom Weapon",
            threeD = false,
            requiredXp = 50,
            rewardXP = 15,
            craftDuration = 120000,
            repairDuration = 15000,
            description = "Custom weapon",
            image = 'weapon_custom.png',
            requiredMaterials = {
                {name = "part1", amount = 1}
            },
            requiredRepairMaterials = { --Required
                {name = "part1", amount = 1}
            }
        }
        ```

