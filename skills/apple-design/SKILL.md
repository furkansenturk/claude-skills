---
name: apple-design
description: >
  Apple's design and UI coding standards in a platform-agnostic form: spacing, target sizes,
  type scale, color and contrast, corner radii, motion and feedback, component behavior, UX
  writing, gestures, keyboard and pointer input, app patterns (accounts, files, media, charts),
  and how to implement them (tokens, scalable text, accessibility, dark mode, reduced motion, RTL).
  Use it when designing, building or reviewing any app UI that should look and feel like Apple's
  (web, Flutter, React Native, Electron, Tauri, SwiftUI), or when asked for Apple-style spacing,
  sizes, typography, animation or interaction standards.
license: MIT
metadata:
  author: furkansenturk
  version: "1.0.0"
---

# Apple design

Values are in pt. 1 pt = 1 px at 1x = 1 dp. Read only the file you need:

| Need | File |
|---|---|
| Spacing, layout, target sizes, type scale, color, contrast, radii, icons | `references/design-tokens.md` |
| Animation, transitions, reduced motion, progress, haptics | `references/motion.md` |
| How a button, nav, sheet, alert, menu, list, form, search… should behave | `references/components.md` |
| Implementing it in code: tokens, scaling text, states, accessibility, RTL | `references/coding.md` |
| Labels, titles, error and empty-state copy, capitalization, inclusive language | `references/writing.md` |
| Gestures, pointer and hover, keyboard shortcuts and focus, drag and drop | `references/input.md` |
| Accounts, help, rating prompts, sharing, files and saving, windows, media, charts, branding | `references/patterns.md` |

Building a whole screen: also read `writing.md`.

## Always

- Use the platform's own components first; style custom ones to match them.
- Put every value in a named token (color role, text style, spacing). No magic numbers.
- Support light and dark appearance, larger text, reduced motion and keyboard use.
- One primary action per view. Destructive actions need a confirmation or undo.
- Cite the file and section when you apply or flag a standard.
