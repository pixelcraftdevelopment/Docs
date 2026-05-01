# Whitelisting Players

* **Purpose:** Restricts access to the crafting system to specific players.
* **Enabling Whitelisting:**
  1. Set Config.Whitelisted to true.
  2. Add players (by their FiveM license identifier) to the Config.WhitelistedPlayers table.
*   **Example:**

    ```
    Config.Whitelisted = true  -- Enables whitelisting
    Config.WhitelistedPlayers = {
        ["license:your_license_identifier_here"] = true, 
        -- Add more players as needed
    }
    ```
* **Adding Players to the Whitelist In-Game:**
  1. Use the /addwhitelistcrafting \[serverid] command in-game (replace \[serverid] with the target player's server ID).
  2. This command will add the specified player's license identifier to the Config.WhitelistedPlayers table in your config.txt.
