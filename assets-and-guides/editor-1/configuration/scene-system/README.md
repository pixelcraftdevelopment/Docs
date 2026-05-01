# Scene System

#### Scene Structure

Each scene is a table with specific properties that control location, animations, and camera work:

```lua
[sceneId] = {
    name = "Scene Name",
    baseLocation = vector3(x, y, z),
    timeOverride = {hour = 22, minute = 30, second = 0}, -- Optional
    ped = {
        -- Ped configuration
    },
    cameraSequence = {
        -- Array of camera shots
    },
    loop = true --for looping animations in sequence
}
```

**Scene Properties**

| Property         | Type    | Required | Description                               |
| ---------------- | ------- | -------- | ----------------------------------------- |
| `name`           | string  | Yes      | Display name for scene identification     |
| `baseLocation`   | vector3 | Yes      | World position for scene center           |
| `timeOverride`   | table   | No       | Override game time (hour, minute, second) |
| `ped`            | table   | Yes      | Character configuration and animations    |
| `cameraSequence` | table   | Yes      | Array of camera movements                 |
| `loop`           | boolean | Yes      | Whether camera sequence loops             |

#### Ped Configuration

```lua
ped = {
    position = vector3(x, y, z),
    heading = 180.0,
    scenario = "WORLD_HUMAN_SMOKING", -- OR animations table
    animations = { -- Optional, replaces scenario
        {
            dict = "anim@amb@nightclub@dancers@crowddance_facedj@",
            anim = "hi_dance_facedj_09_v2_male^5",
            duration = -1, -- -1 for infinite
            flag = 1, -- Animation flags
            blendIn = 2.0,
            blendOut = 2.0
        }
    },
    animationLoop = true,
    requiresPositionLock = true,
    allowedDrift = 1.5 -- Max distance ped can move
}
```

**Ped Properties Explained**

| Property               | Type    | Description                                   |
| ---------------------- | ------- | --------------------------------------------- |
| `position`             | vector3 | Exact world position for ped spawn            |
| `heading`              | float   | Direction ped faces (0-360)                   |
| `scenario`             | string  | Native GTA scenario (simpler than animations) |
| `animations`           | table   | Array of custom animations to play            |
| `animationLoop`        | boolean | Loop through animation array                  |
| `requiresPositionLock` | boolean | Prevent ped from wandering                    |
| `allowedDrift`         | float   | Maximum drift distance if position locked     |

**Animation Properties**

| Property   | Type   | Description                                              |
| ---------- | ------ | -------------------------------------------------------- |
| `dict`     | string | Animation dictionary to load                             |
| `anim`     | string | Animation name within dictionary                         |
| `duration` | number | Duration in ms (-1 for infinite)                         |
| `flag`     | number | Animation flags (0=normal, 1=loop, 2=stop on last frame) |
| `blendIn`  | float  | Blend-in time in seconds                                 |
| `blendOut` | float  | Blend-out time in seconds                                |

#### Camera System

The camera system supports multiple movement types, each with specific parameters:

```lua
cameraSequence = {
    {
        type = "move",
        startPosition = vector3(x, y, z),
        endPosition = vector3(x, y, z),
        startRotation = vector3(pitch, roll, yaw),
        endRotation = vector3(pitch, roll, yaw), -- Optional
        fov = 50.0,
        fovEnd = 45.0, -- Optional
        duration = 10000,
        transitionTime = 2500, -- Optional
        cutStart = 2048, -- Optional
        cutEnd = 6048, -- Optional
        focus = "ped", -- or "manual" or vector3
        focusOffset = {x = 0.0, y = 0.0, z = 0.5},
        focusOffsetEnd = {x = 0.0, y = 0.0, z = 0.7}, -- Optional
        dof = {near = 0.1, far = 20.0, strength = 0.8},
        shake = {amplitude = 0.1, frequency = 0.3, type = "HAND_SHAKE"},
        sway = {amplitude = 0.15, frequency = 0.2}, -- Optional
        effects = {timecycle = "cinema", timecycleStrength = 0.5}
    }
}
```

**Camera Types**

1. **move** - Point A to B movement
   * Required: `startPosition`, `endPosition`, `rotation` or `startRotation`
   * Optional: `endRotation` for rotation during movement
2.  **orbit** - Circular movement around center

    ```lua
    {
        type = "orbit",
        center = vector3(x, y, z),
        radius = 80.0,
        height = 25.0,
        startAngle = 0,
        endAngle = 180,
        duration = 15000
    }
    ```
3.  **crane** - Vertical movement (up/down)

    ```lua
    {
        type = "crane",
        startPosition = vector3(x, y, z),
        endPosition = vector3(x, y, z_higher),
        rotation = vector3(-45.0, 0.0, 90.0)
    }
    ```
4.  **dolly** - Forward/backward with zoom

    ```lua
    {
        type = "dolly",
        startPosition = vector3(x, y, z),
        endPosition = vector3(x_closer, y_closer, z),
        rotation = vector3(pitch, roll, yaw),
        fov = 60.0,
        fovEnd = 30.0 -- Zoom in effect
    }
    ```
5.  **tracking** - Follow predefined path

    ```lua
    {
        type = "tracking",
        path = {
            vector3(x1, y1, z1),
            vector3(x2, y2, z2),
            vector3(x3, y3, z3)
        },
        lookAt = vector3(target_x, target_y, target_z),
        fov = 55.0
    }
    ```
6.  **portrait** - Static close-up shot

    ```lua
    {
        type = "portrait",
        relativePosition = {x = 1.5, y = 2.0, z = 1.4},
        rotation = vector3(-6.0, 0.0, -120.0)
    }
    ```

**Camera Parameters Explained**

| Parameter        | Type           | Description                                      |
| ---------------- | -------------- | ------------------------------------------------ |
| `duration`       | number         | Total shot duration in milliseconds              |
| `transitionTime` | number         | Fade transition time between shots (ms)          |
| `cutStart`       | number         | Start time offset for dynamic cuts (ms)          |
| `cutEnd`         | number         | End time for cut (ms)                            |
| `fov`            | float          | Field of view (10-110, lower = more zoom)        |
| `fovEnd`         | float          | End FOV for zoom effects                         |
| `focus`          | string/vector3 | Focus target: "ped", "manual", or world position |
| `focusOffset`    | table          | Offset from focus target {x, y, z}               |
| `focusOffsetEnd` | table          | End offset for focus transitions                 |

**Depth of Field (DOF)**

```lua
dof = {
    near = 0.1,    -- Near blur distance
    far = 20.0,    -- Far blur distance  
    strength = 0.8  -- Effect strength (0-1)
}
```

* **Near**: Objects closer than this distance blur
* **Far**: Objects farther than this distance blur
* **Strength**: Overall blur intensity (0 = off, 1 = maximum)

**Camera Shake**

```lua
shake = {
    amplitude = 0.15,    -- Shake intensity
    frequency = 0.3,     -- Shake speed
    type = "HAND_SHAKE"  -- Shake pattern
}
```

**Shake Types:**

* `HAND_SHAKE` - Natural handheld camera movement
* `VIBRATE_SHAKE` - Small rapid vibrations
* `DRUNK_SHAKE` - Wobbly, unstable movement
* `ROAD_VIBRATION` - Vehicle-like vibrations

**Camera Sway**

```lua
sway = {
    amplitude = 0.15,  -- Sway amount
    frequency = 0.2    -- Sway speed (breathing rhythm)
}
```

Creates gentle floating movement, simulating breathing or wind.

**Visual Effects**

```lua
effects = {
    timecycle = "cinema",
    timecycleStrength = 0.5
}
```

**Common Timecycles:**

* `cinema` - Cinematic color grading
* `rply_contrast` - High contrast
* `rply_saturation` - Vivid colors
* `Barry1_Stoned` - Hazy, dreamlike
* `tunnel_entrance` - Dark, moody
* `MP_race_finish` - Bright, energetic
