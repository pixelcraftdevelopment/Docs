# Crafting Locations

* **Purpose:** Specifies the locations of crafting tables on your server.
*   **Structure:**

    ```
    {
        name = "Location Name",
        coordinates = {x = 0.0, y = 0.0, z = 0.0, heading = 0.0, radius = 0.0},
        camera = {
            rotation = {x, y, z},
            coords = {x, y, z}
        },
        whitelistedItems = {
            -- Craftable items at this location
        },
        jobs = { -- Allowed job grades or gang grades
            jobname = {
                grades = {1, 2, 3}
            }
        }
    }
    Placeable Tables Configuration
    ============================

    Purpose: Defines craftable placeable tables that players can deploy in-game for crafting.

    Structure:
    {
        [table_name] = {                    -- Unique identifier for the table type(also used in your Inventory items list)
            label = "Display Name",       -- Name shown to players
            whitelistedItems = {},        -- Items craftable at this table
            model = "",                   -- GTA V prop model to spawn
            customHeading = number,       -- Optional: Override default rotation
            jobs = {                      -- Job restrictions
                [job_name] = {
                    grades = {1, 2...}    -- Allowed job grades or gang grades
                }
            }
        }
    }
    Example Usage:
    - Basic tables: Limited crafting for lower-tier jobs
    - Advanced tables: Extended crafting capabilities for higher grades
    - Custom models supported via model property
    - Job-based restrictions through jobs table
    - Optional heading override with customHeading

    Note: Placeable tables complement static crafting locations by allowing
    mobile crafting spots that can be deployed by authorized players.

    ```
* **Adding New Crafting Tables:**
  1. **In-Game:** Use the ingame admin Panel to add new crafting tables for more ease.
  2. **Configuration:**
     * Add a new entry to the Config.CraftingTables table.
     * Paste the recorded x, y, z, and heading values into the location object..
     * **whitelistedItems:** The items array within each table entry determines which iitems can be crafted at that specific crafting table. Modify this array to control which items are available at each location.
