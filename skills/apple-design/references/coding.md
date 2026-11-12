# Coding standards

## Contents
- [Design tokens](#design-tokens)
- [Text](#text)
- [Hit areas and spacing](#hit-areas-and-spacing)
- [Interactive states](#interactive-states)
- [Keyboard and input](#keyboard-and-input)
- [Accessibility semantics](#accessibility-semantics)
- [System preferences](#system-preferences)
- [Layout and safe areas](#layout-and-safe-areas)
- [Right-to-left](#right-to-left)
- [Localization](#localization)
- [Assets](#assets)
- [Permissions and privacy](#permissions-and-privacy)
- [Performance and responsiveness](#performance-and-responsiveness)

## Design tokens
- Define semantic tokens (color, text style, spacing); components reference tokens only, never literal values.
- Name colors by role (label, secondary label, background, separator, accent), not by hue.
- Colors: define light, dark, and increased-contrast variants for every token.
- Use the platform accent/system colors where available; tint sparingly.
- Don't convey meaning by color alone; pair with text, shape, or icon.
- Contrast minimums, checked in light and dark: text up to 17 pt 4.5:1; 18 pt 3:1; bold text 3:1.
- Honor the system appearance (CSS prefers-color-scheme); don't add an app-only toggle.
- Don't hard-code color meanings that vary by culture (e.g. up/down = green/red); make them configurable by locale.

## Text
- Use text styles (size, weight, leading as one token); no ad-hoc font sizes.
- Text scales with the user's text-size setting (rem/relative units, OS dynamic type); custom fonts must scale too.
- No fixed heights on text containers; let height grow.
- Wrap; don't truncate. Truncate only secondary text, and keep the full text reachable.
- At large sizes reflow: stack secondary items under text, reduce column count.
- Bold-text setting: honor it; thin custom weights need larger sizes.
- Align text to the interface direction; keep leading comfortable in multiline text.
- Let people enlarge text by at least 200 percent (system setting or in-app control); icons scale with it.

## Hit areas and spacing
- Hit area is independent of visual size: pad invisible area to meet the minimum.
- Touch targets default 44x44 pt, minimum 28x28 pt; pointer-primary UI default 28x28 pt, minimum 20x20 pt.
- Spacing around controls: about 12 pt around bezeled elements, about 24 pt around unbezeled elements.
- Keep targets from overlapping; spacing counts as much as size.

## Interactive states
- Implement every state: default, hover, pressed, focused, disabled, selected.
- Provide immediate visible feedback on press; hover feedback for pointer input.
- Hover styles only for hover-capable pointers.
- Focus ring: not clipped, not overlapping neighboring text; shown for keyboard use.
- Focus indicator always visible and high-contrast (CSS :focus-visible); never remove outlines without replacement.
- Disabled: dimmed and not focusable-by-action, but still readable; expose disabled state to assistive tech.
- Selected state not by color alone.

## Keyboard and input
- Every action reachable by keyboard; logical Tab order following visual order.
- Standard shortcuts (copy, paste, undo, select all, find, close, quit, print, save) keep their meaning; never override.
- Custom shortcuts use modifier keys and don't conflict with system or accessibility shortcuts.
- Escape dismisses transient UI; Return/Enter activates the default action; Space activates focused controls.
- Support arrow keys in lists, menus, tabs, sliders; support pointer, touch, keyboard, and assistive input equally.
- Don't rely on gestures alone; provide a visible alternative to every custom gesture.

## Accessibility semantics
- Every custom control exposes role, name (label), value, and state (ARIA / OS accessibility API).
- Prefer native elements; add semantics only to custom ones.
- Labels are short, describe the purpose, and exclude the control type; don't repeat visible text differently.
- Hints only for non-obvious results; no hint on self-explanatory controls.
- Meaningful images get alt text; decorative images are hidden from assistive tech (empty alt).
- Icon-only buttons need a text label.
- Announce dynamic changes (status, errors) via live regions.
- Group related elements; reading order matches visual and logical order.
- Don't rely on hover/long-press alone to reveal essential content.
- Give each screen a unique, descriptive title and mark section headings as headings for assistive navigation.

## System preferences
- Reduce motion (CSS prefers-reduced-motion): replace large movement, zoom, spin, parallax with fades or remove; keep functionality.
- Reduce transparency (prefers-reduced-transparency): swap translucent/blurred materials for opaque backgrounds.
- Increase contrast: stronger borders, text, separators.
- Bold text: heavier weights throughout.
- Never auto-play motion or video without a pause control; no flashing content.
- Don't use motion as the only feedback; animations are short, interruptible, and purposeful.
- Read preference values live and respond to changes without restart.
- No views or controls that auto-dismiss on a timer; dismiss on an explicit action.

## Layout and safe areas
- Respect safe areas/insets (notches, rounded corners, system bars, home indicator); extend backgrounds to edges, keep content inside.
- Adapt by available width/height (container or media queries, size classes), never by device model or name.
- Support portrait, landscape, resizable windows, split view, and all text sizes.
- Align and group consistently on a grid; keep primary content in the main reading area.
- Scroll rather than clip; no horizontal scroll for primary content.
- Use leading/trailing, start/end, inline-start/inline-end; never left/right.

## Right-to-left
- Set layout direction from locale and mirror the whole layout: order, alignment, padding, navigation flow.
- Mirror: back/forward and next/previous controls, progress bars, sliders, rating controls, text-direction icons (bars), forward/backward motion icons, swipe and transition directions.
- Don't mirror: numerals themselves, photos, illustrations, artwork, logos, universal marks (checkmark), clocks, real-world object icons, media playback controls, musical notation.
- Reverse order of numerals on progress/counting controls; never flip digits.
- Mixed-direction text: use bidi-aware text handling; don't concatenate strings.
- Complex custom icons: mirror components individually; keep handedness of tools; badges that represent UI mirror with UI.
- Align a paragraph (3+ lines) to its own language, not to the interface direction.
- Reverse the alignment of every item in a list together, including items in another script.
- A control that means a real direction ("to the right") or points at a screen area keeps its direction.
- Reverse image order when the order is meaningful (chronological, alphabetical, favorites).

## Localization
- No text in images; no hard-coded strings; externalize all text.
- Flexible widths: translations expand; no fixed-width containers for text.
- Format dates, times, numbers, currency, units, lists, and names by locale; no manual formatting.
- Use locale-aware sorting and plurals; don't build sentences by concatenation.
- Avoid culture-specific icons, gestures, and colors; use inclusive, neutral wording.
- Names and forms: no assumptions about name structure, gender, or title.

## Assets
- Prefer vector (SVG, symbol fonts) for icons; scale with text and weight.
- Raster images supplied at @2x and @3x (or srcset/density variants); never upscale.
- Provide dark and high-contrast variants of assets where color matters.
- Wide-color images only when needed; fall back gracefully to sRGB.
- Icons share one style, weight, and optical size across the app.

## Permissions and privacy
- Request a permission only when the feature needs it, at the moment of use, never on launch.
- Provide clear purpose text stating why and the benefit; app remains usable when denied.
- Explain before the system prompt when the reason isn't obvious.
- Ask for the minimum data needed; collect nothing unneeded.
- Offer alternatives (manual entry, picker) when permission is denied; link to settings for re-enabling.
- Don't require sign-in or accounts before showing value.
- Store passwords and secrets in the OS secure credential store, never in plain files.
- Don't rely on passwords alone: prefer passkeys or platform sign-in and password autofill; add two-factor where passwords remain.

## Performance and responsiveness
- Never block the main/UI thread; run work off-thread asynchronously.
- Show progress for any wait: determinate indicator when length is known, indeterminate otherwise; show content as it loads.
- Keep UI interactive and cancelable during long tasks.
- Respond to input immediately; show skeleton or placeholder instead of blank screens.
- Handle errors in place with a clear message and a recovery action.
