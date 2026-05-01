# Scene Assignment Logic

The system follows this priority order:

1.  **Character-Specific Mapping** (Highest Priority)

    ```lua
    Config.CharacterSceneMappings = {
        ["ABC12345"] = "Underground Fighter" -- citizenid/identifier
    }
    ```
2. **Job-Based Override**
   * Police, ambulance, mechanic, taxi, realestate get job-specific scenes
   * Includes custom clothing per job grade
3. **Random Civilian Scene** (if `Config.EnableRandomScenes = true`)
   * Assigns random scene from available pool
   * Consistent per character (same scene each login)
4. **Default Slot Scene** (Fallback)
   * Uses scene ID matching character slot number

***
