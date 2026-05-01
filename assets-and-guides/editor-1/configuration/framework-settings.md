# Framework Settings

* **Auto-detection**: Checks for `es_extended`, `qb-core`, or `qbx-core`
* **Manual override**: Set to `'ESX'` or `'QBCORE'` to force framework
* **Qbox detection**: Automatically handles Qbox-specific callbacks

```lua
Config.Framework = nil -- Auto-detect framework if nil
Config.UseQbox = GetResourceState('qbx_core') == 'started'
```
