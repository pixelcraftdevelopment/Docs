# Level-Specific Configurations

These tables contain settings for each job level, impacting various aspects of the mission.

```
Config[1] = {
    InitialDriveSpeed = 15.0,
    InitialDriveStyle = 536871556,
    AggressiveDriveSpeed = 30.0,
    AggressiveDriveStyle = 536871476, 
    RandomEventChance=0.2 , 
    MechanicalFailureChance=0.5,
    HeartAttackChance=0.3,
    RandomEventDistance= math.random(),
    VIPModel = Config.VIPModel1,
    VIPCarModel = Config.VIPCarModel1,
    VIPDriver = Config.VIPDriver1,
    vipHealth=800, 
    opposeChance=1,
    PoliceChance=0.2,
    Rewards = Config.CriminalRewards[1], 
    NotifyChance=0.8,
    EnemyAccuracy=90,
    EnemyHealth=200,
    EnemyGun="WEAPON_PISTOL",
    DriverGun="WEAPON_PISTOL",
    distanceUpperLimit=0.9,
    distanceLowerLimit=0.6,
    leaderexpdriversafe=1,
    leaderexpvehiclesafe=1,
    expall=2,
}
-- Similar structure for Config[2] and Config[3]
```

content\_copyUse code [with caution](https://support.google.com/legal/answer/13505487).Lua

**Driving Behavior:**

* **InitialDriveSpeed:** The default speed at which the VIP's driver will drive.
* **InitialDriveStyle:** The driving style code (refer to FiveM Native Reference for codes) dictating the driver's behavior (e.g., cautious, normal, sporty).
* **AggressiveDriveSpeed:** The speed at which the driver will drive when under attack.
* **AggressiveDriveStyle:** The driving style code the driver adopts when under attack.

**Random Events:**

* **RandomEventChance:** The probability of a random event occurring during the mission (between 0 and 1, where 0 is no chance and 1 is guaranteed).
* **MechanicalFailureChance:** The probability of a mechanical failure event happening if a random event is triggered.
* **HeartAttackChance:** The probability of a heart attack event happening if a random event is triggered. **Note:** The sum of MechanicalFailureChance and HeartAttackChance should be less than or equal to 1.
* **RandomEventDistance:** Determines how far into the journey (as a percentage of total distance) a random event can be triggered. A value of math.random() allows for variation within each mission.

**VIP Configuration:**

* **VIPModel:** An array of possible ped models for the VIP. The script randomly selects one model from this list for each mission.
* **VIPCarModel:** An array of possible vehicle models for the VIP's car. The script randomly selects one model from this list.
* **VIPDriver:** An array of possible ped models for the VIP's driver.
* **vipHealth:** The initial health of the VIP.

**Gameplay Parameters:**

* **opposeChance:** The probability of this job being offered to criminals who have the opposition tablet.
* **PoliceChance:** The probability of the police being alerted when the VIP is under attack.
* **Rewards:** References the rewards criminals receive for successfully completing this level job (see Config.CriminalRewards).
* **NotifyChance:** The probability of players with the opposition tablet being notified about this job.
* **EnemyAccuracy:** The accuracy of enemy NPCs attacking the VIP convoy. (0-100, where 100 is perfect accuracy).
* **EnemyHealth:** The health of enemy NPCs.
* **EnemyGun:** The weapon enemies will be equipped with (refer to FiveM Native Reference for weapon hashes).
* **DriverGun:** The weapon the VIP's driver will be equipped with.

**Distance Settings:**

* **distanceUpperLimit:** Upper limit for the distance traveled (as a percentage of total distance) before a random event can be triggered. Used in conjunction with distanceLowerLimit to create a range.
* **distanceLowerLimit:** Lower limit for the distance traveled before a random event can be triggered.

**Experience Points:**

* **leaderexpdriversafe:** Experience points awarded to the team leader if the driver survives the mission.
* **leaderexpvehiclesafe:** Experience points awarded to the team leader if the VIP's vehicle is in good condition (engine health above 100).
* **expall:** Experience points awarded to all team members upon successful mission completion.
