# Inventory System

* **Purpose:** Specifies the inventory system used on your server.
* **Options:**
  * 'qb-inventory': For the qb-inventory resource.
  * 'qs-inventory': For the qs-inventory resource.
  * 'ox\_inventory': For the ox\_inventory resource. **Note:** When using ox\_inventory, weapon names in other config sections should be in ALL CAPS.
  * For any other inventories, you can leave it to 'qb\_inventory'.
    *   **Example:**

        ```
        Config.Inventory = 'qb-inventory'
        ```

