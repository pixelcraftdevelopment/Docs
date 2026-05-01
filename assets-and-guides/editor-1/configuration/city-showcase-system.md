# City Showcase System

*

    The city showcase system creates cinematic flythrough sequences of Los Santos locations. Unlike character scenes, these are designed for showcasing the city environment.

    #### Showcase Structure

    ```lua
    {
        name = "Maze Bank Tower",
        baseLocation = vector3(-75.0, -820.0, 320.0),
        playerOffset = -50.0,
        preloadRadius = 200.0,
        sequences = {
            -- Array of camera sequences
        }
    }
    ```

    **Showcase Properties**

    | Property        | Type    | Required | Description                                                         |
    | --------------- | ------- | -------- | ------------------------------------------------------------------- |
    | `name`          | string  | Yes      | Location name for identification                                    |
    | `baseLocation`  | vector3 | Yes      | Central world position of the showcase area                         |
    | `playerOffset`  | float   | Yes      | Z-axis offset for player position (usually negative to hide player) |
    | `preloadRadius` | float   | Yes      | Radius in game units to preload assets/textures                     |
    | `sequences`     | table   | Yes      | Array of camera movement sequences                                  |

    #### Camera Sequences

    City showcase uses the same camera types as scenes but with additional properties:

    ```lua
    sequences = {
        {
            type = "orbit",
            center = vector3(-75.0, -820.0, 220.0),
            radius = 120.0,
            height = 80.0,
            startAngle = 0,
            endAngle = 120,
            duration = 18000,
            cutStart = 4096,  -- Optional: Start offset
            cutEnd = 8096,    -- Optional: End time
            fov = 45.0,
            shake = {amplitude = 0.35, frequency = 1.2, type = "HAND_SHAKE"},
            dof = {near = 50.0, far = 2000.0, strength = 0.6}
        }
    }
    ```

    **Additional Showcase Camera Types**

    **slowpan** - Gentle panning movement

    ```lua
    {
        type = "slowpan",
        startPosition = vector3(x, y, z),
        endPosition = vector3(x2, y2, z2),
        rotation = vector3(pitch, roll, yaw),
        fov = 45.0,
        duration = 14000
    }
    ```

    **handheld** - Simulated handheld camera

    ```lua
    {
        type = "handheld",
        relativePosition = {x = 1.2, y = 1.8, z = 1.2},
        rotation = vector3(-8.0, 0.0, -140.0),
        fov = 26.0,
        focus = "manual",
        duration = 10000,
        shake = {amplitude = 0.04, frequency = 0.3, type = "HAND_SHAKE"},
        sway = {amplitude = 0.15, frequency = 0.2}
    }
    ```

    #### Timing and Cuts

    The `cutStart` and `cutEnd` parameters allow for dynamic camera cuts:

    ```lua
    {
        duration = 20000,     -- Total sequence duration (20 seconds)
        cutStart = 5000,      -- Start showing at 5 seconds
        cutEnd = 15000,       -- Stop showing at 15 seconds
        -- Camera will be active for 10 seconds (5s to 15s)
    }
    ```

    This system can be used to create synchronized cuts with music or other timing requirements:

    * Calculate timing based on tempo (e.g., 117 BPM = 512ms per beat)
    * Use multiples of beat duration for `cutStart` and `cutEnd`
    * Example: `cutStart = 2048` (4 beats), `cutEnd = 6144` (12 beats)
