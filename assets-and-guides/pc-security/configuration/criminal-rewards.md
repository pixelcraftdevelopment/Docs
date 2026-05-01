# Criminal Rewards

This table defines rewards that criminals receive for successfully hijacking VIP missions. The rewards are categorized by job level.

```
Config.CriminalRewards = {
    [1] = {  -- Level 1 Rewards
        { 
            item = "weapon_pistol", --Spawncode
            chance = 0.9,  -- Chance of getting reward
            quantity = {1, 2, 3, 4}  -- Quantities for team sizes 1-4 
        },
    }
}
```

content\_copyUse code [with caution](https://support.google.com/legal/answer/13505487).Lua

* **\[1], \[2], \[3]:** Represent job difficulty levels.
  * **item:** The spawncode of the reward item.
  * **chance:** The probability (between 0 and 1) of the criminal receiving this specific reward.
  * **quantity:** A table defining the quantity of the item awarded based on the criminal team size. For instance, quantity = {1, 2, 3, 4} means a solo criminal gets 1, a team of 2 gets 2, and so on.
