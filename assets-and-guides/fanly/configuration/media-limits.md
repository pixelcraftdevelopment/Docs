# Media Limits

Controls which image and video URLs are accepted in posts and DMs. Validation is server-side — the UI also enforces these so users get fast feedback.

```lua
Config.Media = {
    imageExtensions = { 'jpg', 'jpeg', 'png', 'gif', 'webp', 'avif' },
    videoExtensions = { 'mp4', 'webm' },
    maxDurationSec  = 600,
}
```

## imageExtensions

Lower-cased extension whitelist. Matched against the URL path (query strings are ignored). Default covers all modern browser-supported formats.

To allow extra formats:

```lua
Config.Media.imageExtensions = { 'jpg', 'jpeg', 'png', 'gif', 'webp', 'avif', 'bmp' }
```

## videoExtensions

Default is intentionally narrow:

* `mp4` and `webm` have the most consistent decode coverage across the CEF builds the various phone hosts ship with.
* `mov` and `m4v` sometimes work but routinely show up as black boxes on stock CEF.

Add extra extensions only after confirming on your players' actual phone host:

```lua
Config.Media.videoExtensions = { 'mp4', 'webm', 'mov' }
```

## maxDurationSec

Maximum allowed video length in seconds.

* `0` — no duration enforcement.
* Default `600` (10 minutes).

Note that duration enforcement requires the URL host to expose duration metadata (most CDN-hosted videos do via HEAD requests). If duration can't be determined, the post still goes through — only confirmed-too-long uploads are rejected.
