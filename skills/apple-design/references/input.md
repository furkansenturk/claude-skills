# Input

## Contents
- [Standard gestures](#standard-gestures)
- [Custom gestures](#custom-gestures)
- [Pointer](#pointer)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Keyboard navigation and focus](#keyboard-navigation-and-focus)
- [Drag and drop](#drag-and-drop)
- [Text selection and editing](#text-selection-and-editing)

## Standard gestures
| Gesture | Expected action |
|---|---|
| Tap / click | Activate a control; select an item |
| Double tap / double click | Zoom in (out if zoomed); open an item; select a word while editing |
| Swipe | Reveal actions; dismiss views; scroll |
| Drag | Move a UI element |
| Long press | Reveal additional controls (context menu); then drag to move |
| Pinch | Zoom / magnify |
| Two-finger rotate | Rotate selected item |
| Swipe from the side | Go back (shortcut only; keep a Back button) |
| Three-finger swipe left / right | Undo / redo |
| Three-finger pinch in / out | Copy / paste selected text |
| Shake | Undo / redo |

- Same gesture, same result in every context; never give a familiar gesture an app-unique meaning or invent one for a standard action.
- Respond immediately; show feedback during the gesture that predicts its result.
- Show unavailable gestures (locked item, disabled control) distinctly.
- Always offer alternatives: keyboard, voice, assistive input.
- Don't redefine system-wide gestures.
- On pointer-first UI with touch: keep layout and control size; enlarge hit targets, not controls; give touch equivalents for modifier-key or hover actions.

## Custom gestures
- Only for specialized, frequent tasks standard gestures don't cover (drawing, games).
- Discoverable, simple, distinct from other gestures, never the only way to do an important action.
- Supplement standard controls, never replace them.
- Work for both touch and pointer; use modifier keys where needed.
- Don't conflict with system gestures.

## Pointer
- Primary click selects or activates; secondary click (or Control-click) opens the context menu.
- Modifier-drag (e.g. Option to duplicate) gives the same result for touch and pointer.
- Hover reveals auto-hiding controls (minimized toolbars, playback controls); leaving hides them.
- Hover feedback on every interactive element, standard effects only, never decorative: highlight for a group of controls in a shared container; lift (scale up + shadow) for a standalone or small opaque element; hover (custom scale, tint, shadow) for large elements. No scaling where neighbors crowd (table rows); use tint.
- Pad interactive elements for comfortable hit regions; adjacent bar buttons' hit regions contiguous.
- Keep custom pointer shapes simple; no instructional text.

| Pointer shape | Use when |
|---|---|
| Arrow | Default |
| Pointing hand | Over a link |
| I-beam | Text selection/insertion possible |
| Cross | Precise rectangular selection |
| Open / closed hand | Content draggable / being dragged |
| Resize (horizontal, vertical, diagonal) | Over a draggable edge, divider, corner; one-direction variant at a limit |
| Copy | Drop will duplicate (Option held) |
| Link | Drop will create a reference |
| Context menu | Context menu available (Control held) |
| Not allowed | Can't drop here |

## Keyboard shortcuts
| Shortcut | Action |
|---|---|
| Cmd/Ctrl-A | Select all |
| Cmd/Ctrl-C / X / V | Copy / cut / paste |
| Cmd/Ctrl-Z | Undo |
| Shift-Cmd/Ctrl-Z | Redo |
| Cmd/Ctrl-F | Find |
| Cmd/Ctrl-G | Find next |
| Shift-Cmd/Ctrl-G | Find previous |
| Cmd/Ctrl-N / O / S / P | New / open / save / print |
| Cmd/Ctrl-W | Close window |
| Cmd/Ctrl-Q | Quit |
| Cmd/Ctrl-B / I / U | Bold / italic / underline |
| Cmd/Ctrl-, | Settings |
| Esc | Cancel |
| Shift-Tab | Focus backward |
| Shift-Left/Right | Extend selection one character |
| Alt-Shift-Left/Right (Apple keyboards), Ctrl-Shift-Left/Right (others) | Extend selection by word |

- Never repurpose a standard shortcut (only if its action is meaningless in the app); never add a modifier to one for an unrelated command.
- Custom shortcuts only for the most frequent app-specific commands.
- Modifiers: primary is Cmd on Apple keyboards, Ctrl elsewhere; Shift for a related variant of a shortcut; Alt/Option sparingly for rare commands. Combine extra modifiers only with letters.
- List multiple modifiers in one consistent order everywhere.
- Don't add Shift for a key's upper character (Cmd/Ctrl-?, not Shift-Cmd/Ctrl-/).
- Cmd/Ctrl while dragging moves items as a group; Shift while resizing keeps aspect ratio; holding an arrow key nudges the selection by the smallest unit.
- Show shortcuts in main menus, not context menus.

## Keyboard navigation and focus
- Everything reachable and operable by keyboard alone.
- Tab moves between focus groups (sidebars, grids) in reading order (leading to trailing, top to bottom); arrow keys move among items within a group. Fix custom views' order if wrong.
- A group gaining focus focuses its primary (most likely) item.
- Never move focus without user action, except after directional input when the focused item disappears.
- Focusing may also select, unless selection shifts context (opening a view); then require separate activation.
- Use the platform's focus effect: ring for text and search fields (and items filling a cell, like photos); full-row highlight for list and collection items (focused: accent background, white text; unfocused: gray background, normal text).
- With full keyboard access, controls need no custom focus; content elements (list items, fields) do.

## Drag and drop
- Support wherever users may try it; offer alternatives (menu commands, assistive support).
- Same container moves; different container or app copies. Option/Alt at drop forces copy within one container; check at drop time.
- Show a translucent drag image after about three points of movement until drop; adapt it to preview the result; group multiple items and ungroup on drop.
- Highlight or show an insertion point only while over a valid destination; for invalid, show nothing or not-allowed.
- Failed drop: animate back to the source, or scale up and fade out.
- Auto-scroll scrollable destinations during drag.
- Support multi-item drag, and adding items to an in-progress drag.
- Make drops undoable; confirm first if not.
- Offer representations highest to lowest fidelity; accept the richest supported; extract only the relevant part. Keep dropped text style if destination supports it, else use the destination's.
- After a drop keep content selected in the destination; remove from source on move.
- Spring loading: dragging over a button or segmented control activates it.

## Text selection and editing
- Let users select and copy noneditable content text, not control labels.
- Edit menu via the platform's usual reveal (long press, double tap, secondary click); no custom reveal or duplicate controls.
- Show only relevant commands (no Copy/Cut without selection, no Paste when empty); custom ones after system ones, few, short verb labels.
- Support undo and redo; no confirmation for edit commands.
- Context menu: few relevant items, at most about three groups, one submenu level, hide (don't dim) unavailable items, frequent items nearest the reveal point, destructive items last and marked, every item also in the main interface, title only if it clarifies.
