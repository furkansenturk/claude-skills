# Design tokens

## Contents
- [Layout](#layout)
- [Target sizes](#target-sizes)
- [Typography](#typography)
- [Color](#color)
- [Dark mode](#dark-mode)
- [Corner radius](#corner-radius)
- [Materials and elevation](#materials-and-elevation)
- [Icons and symbols](#icons-and-symbols)
- [App icon](#app-icon)
- [Images](#images)

## Layout
- Layout basis: size classes (compact/regular width and height), not device type or orientation
- Live-activity-style card margin: 14 pt
- Critical controls: not at the bottom edge of a resizable window
- Spacing: consistent across a layout; group with whitespace, containers or separators
- Controls in a row: max 3 glyph buttons or 2 text buttons
- Partially clipped offscreen content: same visible width on both sides
- Background artwork: keep aspect ratio, scale to fill, never letterbox
- Resizing: support it; reflow instead of fixed sizes
- Adjacent views at large text: stack vertically; rows grow taller
- Most important content at the top and leading side; indent to mark subordinate items.
- Keep functionality the same at every size; change only how much is shown.

## Target sizes
| Input | Default | Minimum |
|---|---|---|
| touch | 44x44 pt | 28x28 pt |
| pointer | 28x28 pt | 20x20 pt |

- Padding around controls with a bezel: about 12 pt
- Padding around controls without a bezel: about 24 pt
- Button heights (large-control scale): 28, 32, 44, 52, 64 pt
- Gaze/hover-driven controls: centers at least 60 pt apart; 4 pt padding if control is 60 pt or larger

## Typography
- Default body size: 17 pt touch, 13 pt pointer
- Minimum text size: 11 pt touch, 10 pt pointer
- Weights: Regular, Medium, Semibold, Bold; avoid Ultralight, Thin, Light
- Typefaces: minimize; hierarchy via weight, size, color
- Emphasized variants get their own token; don't override weight or size at the use site
- Emphasized variant weight: Medium, Semibold, Bold or Heavy as listed

Compact (phone-size) text styles at default text size (size / leading in pt):

| Style | Weight | Size | Leading | Emphasized |
|---|---|---|---|---|
| Large Title | Regular | 34 | 41 | Bold |
| Title 1 | Regular | 28 | 34 | Bold |
| Title 2 | Regular | 22 | 28 | Bold |
| Title 3 | Regular | 20 | 25 | Semibold |
| Headline | Semibold | 17 | 22 | Semibold |
| Body | Regular | 17 | 22 | Semibold |
| Callout | Regular | 16 | 21 | Semibold |
| Subhead | Regular | 15 | 20 | Semibold |
| Footnote | Regular | 13 | 18 | Semibold |
| Caption 1 | Regular | 12 | 16 | Semibold |
| Caption 2 | Regular | 11 | 13 | Semibold |

Regular (desktop) text styles:

| Style | Weight | Size | Leading | Emphasized |
|---|---|---|---|---|
| Large Title | Regular | 26 | 32 | Bold |
| Title 1 | Regular | 22 | 26 | Bold |
| Title 2 | Regular | 17 | 22 | Bold |
| Title 3 | Regular | 15 | 20 | Semibold |
| Headline | Bold | 13 | 16 | Heavy |
| Body | Regular | 13 | 16 | Semibold |
| Callout | Regular | 12 | 15 | Semibold |
| Subhead | Regular | 11 | 14 | Semibold |
| Footnote | Regular | 10 | 13 | Semibold |
| Caption 1 | Regular | 10 | 13 | Medium |
| Caption 2 | Medium | 10 | 13 | Semibold |

Dynamic text scaling, compact (phone-size) Body size / leading and Large Title size / leading:

| Setting | Body | Large Title |
|---|---|---|
| xSmall | 14 / 19 | 31 / 38 |
| Small | 15 / 20 | 32 / 39 |
| Medium | 16 / 21 | 33 / 40 |
| Large (default) | 17 / 22 | 34 / 41 |
| xLarge | 19 / 24 | 36 / 43 |
| xxLarge | 21 / 26 | 38 / 46 |
| xxxLarge | 23 / 29 | 40 / 48 |
| AX1 | 28 / 34 | 44 / 52 |
| AX2 | 33 / 40 | 48 / 57 |
| AX3 | 40 / 48 | 52 / 61 |
| AX4 | 47 / 56 | 56 / 66 |
| AX5 | 53 / 62 | 60 / 70 |

- Text scaling: all text follows the user text-size setting; every style scales, including the smallest (Caption 2: 11 pt at default, 40 pt at AX5)
- Scaling priority: keep primary content readable first; do not need to enlarge every word
- Hierarchy: keep relative size and weight distinctions at every text size
- Tracking: tighter as size grows; small sizes need positive tracking (e.g. 11 pt: +0.06 pt, 10 pt: +0.12 pt, 6 pt: +0.24 pt)

## Color
- Semantic colors: use dynamic roles (label primary/secondary/tertiary/quaternary, system backgrounds base/elevated, separators, fills); do not hard-code system color values
- Semantic meaning: one color = one meaning; do not redefine system roles
- Appearances: every color works in light, dark and increased-contrast variants
- Contrast, text up to 17 pt: at least 4.5:1
- Contrast, text 18 pt: at least 3:1
- Contrast, bold text: at least 3:1
- Contrast in dark mode: at least 4.5:1; aim for 7:1 for custom small text
- Increase-contrast setting (CSS prefers-contrast / OS setting): provide a higher-contrast scheme if default misses minimums
- Color only: never the sole carrier of status, interactivity, focus or required information; pair with text, shape or symbol
- Color use: sparingly; prefer bold text and large areas; avoid color on light-weight or small text
- Similar colors: avoid overlapping similar colors in controls and content layer
- Color space: include a color profile; sRGB base, P3 for wide color with sRGB fallback
- Disabled text and placeholders: clearly fainter than enabled text and entered values

## Dark mode
- Appearance: follow the system setting; no app-specific appearance switch
- Backgrounds: system background colors; elevated surfaces (popovers, sheets) switch from base to elevated variant
- White-background images: darken slightly
- Icons and images: same asset if it works in both; otherwise ship light and dark variants
- Test: dark mode combined with Increase Contrast and Reduce Transparency, separately and together

## Corner radius
- Corners: concentric (nested rounded shapes share a center with their container)
- Concentric: inner radius = outer radius - inset
- Rounded shapes: match device and container curvature; do not hard-code unrelated radii
- Preferred button shapes for gaze/hover input: circular or capsule

## Materials and elevation
- Controls vs content: glass/translucent material for the controls layer only; never in the content layer
- Glass effects: sparingly; standard components inherit them
- Clear glass variant: only over visually rich backgrounds
- Dimming layer behind clear glass over bright content: 35% opacity dark
- Standard materials: choose by semantic purpose, not apparent color; thicker = more opaque = better contrast for fine text
- Text and fills on materials: vibrant label colors; avoid quaternary on thin and ultra-thin materials
- Color on glass: sparingly; reserve for status or primary emphasis
- Windows: prefer translucency to opaque fills

## Icons and symbols
- Symbol weights: nine, ultralight to black; match adjacent text weight
- Symbol scales: small, medium (default), large; relative to text cap height
- Symbol size: same point size as adjacent text keeps weight match; change scale for emphasis
- Small sizes: enclosed shapes (circle, square) improve legibility
- Rendering modes: monochrome, hierarchical, palette, multicolor; check each in every context
- Document icon center image: margin about 10% of canvas, artwork about 80% (205x205 px in 256x256 px)
- Document icon sizes (px @1x / @2x): 512 / 1024, 256 / 512, 128 / 256, 32 / 64, 16 / 32
- Simplify detail at small sizes
- Optically center asymmetric icons with padding, not geometric centering.

## App icon
- Master size: 1024x1024 px, square, unmasked layers; system applies rounded mask
- Layers: square, unmasked; keep primary content centered
- Variants: default, dark, clear light, clear dark, tinted light, tinted dark
- Artwork: illustration over photo; no replicated UI components; avoid extremely thin lines
- Crisp edges on foreground shapes (no soft or feathered edges); keep core features the same in every appearance variant.

## Images
- Scale factors: touch phone @2x and @3x; touch tablet @2x; desktop @1x and @2x
- Authoring: design at lowest resolution, scale up; vector control points on whole values at 1x
- Include a color profile in each image
- Layered images: keep text in foreground; background layer opaque
- Text over an image must stay legible: add a shadow or a background layer.
