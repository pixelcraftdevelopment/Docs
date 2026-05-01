# Character Slot Management

```lua
Config.DefaultNumberOfCharacters = 5
Config.PlayersNumberOfCharacters = {
    { license = "license:xxxxxxxx", numberOfChars = 10 },
}
```

* **Default slots**: Applied to all players
* **Per-player overrides**: Based on Rockstar license (40 characters)
* **License format**: `license:` followed by 40 hex characters
