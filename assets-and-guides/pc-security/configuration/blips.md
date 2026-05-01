# Blips

This table allows you to define custom blips on the map for points of interest related to security operations.

```
Config.Blips = {
    { name = "Hospital", coords = vector3(304.21, -600.45, 57.95) },  
    { name = "Police", coords = vector3(450.53, -983.76, 43.69) },
    -- ...
}
```

content\_copyUse code [with caution](https://support.google.com/legal/answer/13505487).Lua

* **name:** The name of the location displayed on the blip.
* **coords:** The vector3 coordinates of the blip's location.

**Note:** You need to add the corresponding blip images to the security/html/build/images directory. The filenames should match the blip names (e.g., "Hospital.png", "Police.png").
