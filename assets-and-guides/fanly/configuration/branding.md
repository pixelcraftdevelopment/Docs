# App Branding

Rebrand Fanly for your server — change the launcher name, description, and icon.

```lua
Config.App = {
    name        = 'Fanly',
    description = 'Subscribe to your favorite creators',
    icon        = 'https://cfx-nui-fanly/ui/dist/FanlyLogo.png',
}
```

## name

The label shown under the icon in the phone's app launcher.

## description

Short tagline shown on phones that display app descriptions (e.g. lb-phone's app drawer).

## icon

URL to the icon image. The default points at the bundled `FanlyLogo.png` inside the resource (no external host needed).

* **Most phones** (lb-phone, yseries, gksphone, qs-smartphone, qb-phone, npwd) — use a PNG. Recommended size: 512×512, square, transparent background.
* **17mov_Phone** — uses an SVG instead. The 17mov branch in the resource overrides the PNG with `ui/public/icon.svg` automatically because 17mov inlines icons as DOM markup (a PNG would paste raw bytes).

To swap your own icon:

1. Drop your PNG into `fanly/ui/public/` (e.g. `MyBrand.png`).
2. Update `Config.App.icon` to point at it: `'https://cfx-nui-fanly/ui/dist/MyBrand.png'`.
3. Rebuild the UI: `cd fanly/ui && npm run build`.
4. Restart the resource.

For 17mov, also drop a square SVG into `fanly/ui/public/icon.svg` and rebuild.

## Sender Labels

These also affect how the brand appears on outbound notifications — see [Push Channel & Sender Labels](push-channel.md).
