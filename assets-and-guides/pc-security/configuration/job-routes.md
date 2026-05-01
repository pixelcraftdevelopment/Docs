# Job Routes

```
Config.JobRoutes = {
    EscortVIP = { 
        [1] = {  -- Routes for Level 1 jobs
            {start_coord = vector4(-59.44, -1628.19, 29.18, 140.64), end_coord = vector3(-1079.02, -2982.52, 13.95)},
            -- More routes for Level 1...
        },
        [2] = {  -- Routes for Level 2 jobs
            -- ...
        },
        [3] = {  -- Routes for Level 3 jobs
            -- ...
        },
    },
}
```

content\_copyUse code [with caution](https://support.google.com/legal/answer/13505487).Lua

* **EscortVIP:** Represents the mission type. In this case, it's escorting a VIP.
* **\[1], \[2], \[3]:** Represent job difficulty levels, ranging from 1 (easiest) to 3 (hardest).
  * **start\_coord:** The starting point of the route, defined as a vector4. The fourth value (W) indicates the initial heading of the VIP's vehicle.
  * **end\_coord:** The destination of the route, defined as a vector3.

**Example:**

```
{start_coord = vector4(-59.44, -1628.19, 29.18, 140.64), end_coord = vector3(-1079.02, -2982.52, 13.95)}
```
