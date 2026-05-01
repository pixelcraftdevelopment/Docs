# Whitelisted Admins

* **Purpose:** Restricts access to the admin panel and the UI to certain admins.
* **Enabling Whitelisting admins:**
  1.  Add players (by their FiveM license identifier) to the Config.WhitelistedAdmins

      &#x20;table.
*   **Example:**

    ```
    Config.WhitelistedAdmins = {
        "license2:e029f99cc4975eebb22d974c762013772ebf5e07",
        "license:e029f99cc4975eebb22d974c762013772ebf5e08" --You can add more
        --Use licence2 in QBOX, just licence in Qbcore and for ESX, use character identifiers, eg.,char1:e029f99cc4975eebb22d974c762013772ebf5e07 
    }
    ```
