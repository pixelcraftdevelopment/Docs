# UI Editor

## What is the UI Editor?

The UI Editor is a built-in live style customization tool that lets server owners and admins modify the visual appearance of the crafting interface without touching any code. Changes apply in real-time and can be saved as named profiles.

Access the UI Editor from within the crafting interface (admin only). The editor opens as an overlay on top of the game UI.

## Style Editor Tabs

The Style Editor panel has six tabs:

- **Global:** Server-wide settings: text colors, font sizes, font weights, font families, landing page background, logo settings
- **Style:** Component-specific background, opacity, gradient, and image settings
- **Border:** Border style (solid/dashed/dotted/none), width, color, and radius
- **Hover:** Hover effects — border, background, scale, rotation, and shadow on hover
- **Animate:** Entry animation style — Smooth Fade, Slide Up, Scale, Bounce, Rotate
- **SVG Editor:** Paste custom SVG code for UI icons

## Background Options

The landing page and component backgrounds support three types:

- **Solid Color:** Pick a single RGBA or HEX color using the color wheel
- **Gradient:** Choose Linear or Radial gradient with custom colors and angle
- **Image:** Paste a direct image URL as the background. Right-click any image → "Copy image address" → paste in the Image URL field

## Style Profiles

Profiles let you save and load complete style configurations:

- **New Profile:** Enter a name and create a new style profile from current settings
- **Load Profile:** Select a saved profile to restore its settings
- **Save (Overwrite):** Save changes to the current profile
- **Delete Profile:** Remove a saved profile
- **Reset:** Reset a specific component's settings back to default
- **Global Reset:** Reset ALL styling preferences to default

Profile data saves server-side in `dist/ui-config.json` and persists across server restarts. The "Unsaved changes" indicator appears when there are pending modifications.

## Color Picker

The built-in color wheel supports two modes:

- **RGBA mode:** Enter Red, Green, Blue, Alpha values (0–255 / 0–1)
- **HEX + Alpha mode:** Enter a 6-digit hex color code plus alpha

Use `↑` / `↓` arrow keys to fine-tune numeric values. Use the Preview buttons to see hover and animation effects before applying.
