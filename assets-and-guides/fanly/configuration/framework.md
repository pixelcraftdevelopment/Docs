# Framework, Phone, Locale

Top-level runtime settings in `fanly/config.lua`.

## Framework

```lua
Config.Framework = 'auto'   -- 'auto' | 'QBCore' | 'Qbox' | 'ESX'
```

* `'auto'` detects framework by started resources at runtime.
* Set explicit value if your server has multiple framework resources present.

## Phone

```lua
Config.Phone = 'auto'   -- 'auto' | 'lb-phone' | 'yseries' | 'gksphone' | 'qs-smartphone' | 'qs-smartphone-pro' | 'qb-phone' | '17mov_Phone' | 'npwd'
```

* `'auto'` registers against whichever phone resource is started first.
* Override only if you run more than one phone resource and want to pin Fanly to a specific one.

## Notifications

```lua
Config.Notifications = 'auto'   -- 'auto' | 'ox_lib' | 'okokNotify' | 'ps-ui' | 'lation_ui' | 'nox_notify'
```

Used for in-game toast notifications. Phone pushes use the phone's own native notification system, independent of this setting.

## Locale

```lua
Config.Locale = 'en'   -- en, es, fr, de, it, pt, sv, ja, cn, ar
```

Selects which locale file is loaded. Add new locales by dropping a `<code>.lua` into `fanly/locales/` following the same key set as `en.lua`.

## Debug

```lua
Config.Debug = false
```

Enables additional debug logging. Off in production.
