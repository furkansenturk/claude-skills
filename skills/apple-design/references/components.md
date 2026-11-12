# Components and flows

## Contents
- [Buttons](#buttons)
- [Navigation](#navigation)
- [Modality](#modality)
- [Menus and context menus](#menus-and-context-menus)
- [Lists and tables](#lists-and-tables)
- [Text fields and forms](#text-fields-and-forms)
- [Toggles, segmented controls, pickers, sliders](#toggles-segmented-controls-pickers-sliders)
- [Search](#search)
- [Progress, loading, empty states](#progress-loading-empty-states)
- [Toolbars](#toolbars)
- [Notifications and permissions](#notifications-and-permissions)
- [Onboarding and launch](#onboarding-and-launch)
- [Settings](#settings)
- [Undo and destructive actions](#undo-and-destructive-actions)

## Buttons
- Hit region at least 44x44 pt. Custom buttons need a press state.
- One prominent-style button per view for the most likely action. Distinguish preferred choice by style, not size.
- Roles: normal, primary (default), cancel, destructive. Never give primary role to a destructive action, even if most likely.
- Label states the purpose; use text when a short label is clearer than an icon; familiar icons for familiar actions.
- Long-running action: show an activity indicator inside the button.
- Append an ellipsis to the title when the button opens another window, view, or app (pointer UI).

## Navigation
- Tab bar: top-level sections only, never actions. Always visible during navigation. Fewer tabs is better; icon plus label on each.
- Never disable or hide a tab; if a section is empty, explain why.
- Avoid overflow: trailing tab becomes a "More" tab that hides content.
- Badge only for critical information.
- Regular (tablet/desktop) width: sidebar for complex apps, may adapt from tab bar. Prefer a tab bar first; use a sidebar within a tab for deep hierarchy.
- Sidebar: at most two levels of hierarchy; no critical information or actions at the bottom; let people hide it.
- Title bars: concise title, under 15 characters; do not use the app name; use the standard Back and Close buttons.
- Sidebar: let people customize its items; hide it automatically when the window gets narrow.
- Split view: regular width only (one pane at compact width); keep the current selection highlighted in every pane leading to the detail.
- Tabbed panes: no more than six tabs; controls in a pane affect only that pane.
- Desktop menu bar: list every app command there, even ones available elsewhere.

## Modality
- Use modal only with a clear benefit; keep tasks simple, short, streamlined. Always an obvious way to dismiss. Confirm before closing if data would be lost.
- One sheet at a time from the main interface; never more than one alert at once.
- Sheet: scoped task tied to current context. Cancel/Close dismisses without saving; Done saves and dismisses. Pair Done with Cancel (or Back). Support swipe-down dismiss; include a grabber on resizable sheets.
- Multi-step sheet: first step Cancel plus inactive Done; later steps Back; final step Back plus active Done.
- Alert: critical, immediate information only. Title, optional message, up to three buttons. Never at launch; not for common undoable actions or plain information.
- Alert titles: short, direct, neutral. No explaining buttons. Button titles are specific verbs; avoid "OK" unless purely informational.
- Alert with destructive action: include Cancel. Offer another way to cancel where sensible. Avoid scrolling alerts. Let people suppress repeating alerts.
- Confirmation dialog (action sheet): choices for an intentional action. At most four buttons including Cancel (three choices). Short single-line title; message only if needed; destructive choices at the top and visually prominent, Cancel at the bottom; no scrolling.
- Popover: small, transient content; one at a time, never stacked or cascaded; arrow points at its origin without covering it; size to content. Not for warnings. In compact width use a sheet instead.
- Give every modal view a title or short text that names its task.
- Alert button order: most likely choice trailing in a row or top in a stack; Cancel is titled "Cancel" and is never the default.
- Destructive style only for a destructive action people didn't deliberately choose (a deliberate "Empty Trash" keeps the normal style).
- A nonmodal popover that closes on an outside tap or click saves the person's work; discard only on an explicit cancel.

## Menus and context menus
- Labels: concise, title-style capitalization, no articles. Append an ellipsis when more input is needed before the action completes.
- Dim unavailable items; keep the menu itself enabled.
- Most important/frequent items first; group related items; separators for at most about three groups.
- Submenus sparingly; one level; if over about five items, make a separate menu.
- Checkmark for an attribute in effect; changeable label for current state ("Show"/"Hide").
- Context menu: few, relevant items; every item also reachable in the main interface; destructive items marked; shortcuts shown only in main menus; context menu or edit menu per item, not both; keep height within the window.
- Reserve the ellipsis (…) icon for the overflow menu; give other menus a distinct icon.
- Icons on all items of a group or on none. Keep related commands in one group even if used at different frequencies.
- Keep a submenu enabled even when all its items are unavailable.
- Button with an action menu: at least three items, otherwise use buttons; never hide all of a view's primary actions in it.
- Selection menu: show a useful default and a label that predicts the options.

## Lists and tables
- Prefer text in rows; keep row text succinct; show selection feedback.
- Multi-column: descriptive headings; sortable by heading; resizable columns.
- Hierarchical data: outline view, not a table.
- Info (detail) button reveals more about a row; it does not navigate.
- No index when rows have trailing controls. Limit row count when possible.
- Editing requires an edit mode on touch before rows can be selected.
- Narrow columns: truncate in the middle to keep the start and end visible.
- Clicking an already-sorted column heading reverses the sort.
- Don't change a collection's layout while people view it unless they asked for it.

## Text fields and forms
- Text field for small, specific text; size to expected input.
- Label every field; placeholder gives a hint only, never the sole label.
- Offer choices (pickers, toggles) instead of typing where possible; support paste and drag-drop; pull data from the system instead of asking.
- Secure field for private data; never prepopulate a password.
- Validate at the right time: formats like email when focus leaves the field; usernames and passwords while typing. Mark required fields; explain errors.
- Showing a field message must not move neighboring controls.
- Enable Next/Continue only after the required fields are filled.
- Show the keyboard type matching content (numeric, email, URL). Logical tab order between fields.
- Trailing clear button. Combo box when text input needs a list of choices.

## Toggles, segmented controls, pickers, sliders
- Toggle: two opposing states, clear label of what it controls. Switch only in list rows; outside lists use a toggle-style button. Checkbox for a single on/off setting or hierarchies; radio buttons for mutually exclusive sets (keep short).
- Segmented control: closely related choices affecting a view or object. About five to seven segments wide, about five or fewer in compact width. Noun labels; text or images, not mixed; equal widths.
- Picker: medium-to-long lists of ordered values; show in context (below field or popover), not a new view.
- Date picker: compact style when space is tight; minute interval must divide evenly into 60 (e.g. 15); countdown max 23:59.
- Slider: continuous range; min leading/bottom, max trailing/top; live feedback; optional text field plus stepper; label min and max at least; tick marks for precision. Not for volume.
- More than about five mutually exclusive options: use a pop-up or dropdown, not radio buttons.
- A parent checkbox shows a mixed state when its children differ.
- A segmented control is all selections or all actions, never mixed.

## Search
- Placeholder says what can be searched. Search as typing starts; show suggestions.
- Broader scope by default; refine with a scope bar (clear categories) or tokens (common terms).
- Place at bottom if room, at top when there is no bottom toolbar or bottom content needs space.
- Search tab: standard style for discovery and suggestions, button style for quick lookup.
- Most relevant results first; group results into categories. In a dedicated search area, focus the field on arrival.

## Progress, loading, empty states
- Spinner for background or space-constrained operations. Bar for measurable tasks.
- Description gives context; avoid vague "Loading".
- Consistent indicator location. Let people cancel; warn if cancelling has consequences.
- Show something immediately; let people keep working while loading; refresh content automatically.
- Empty section: explain why it is empty; do not disable or hide its entry point.

## Toolbars
- Frequent commands only; avoid overcrowding; overflow goes in a More menu.
- Group by function and frequency. Leading: back/sidebar toggle then title. Trailing: key actions, search, More.
- Prefer standard symbols without borders; prominent style only for Done/Submit.
- Each control's meaning is clear; hide toolbars only with a reliable way to restore them.
- At most three groups of controls. On desktop, every toolbar command also exists in the menu bar.

## Notifications and permissions
- Four levels: passive, active (default), time-sensitive, critical (extremely rare, urgent health/safety). Match urgency accurately.
- Time-sensitive only when relevant in the moment; never for marketing.
- Explicit permission before marketing notifications; provide in-app notification settings.
- Request permission when the feature is first used, or in onboarding if required to function; explain the benefit first.
- Never send several notifications for the same thing; show errors in an alert, not a notification.
- No sensitive or personal data in notification text.
- App badge counts unread notifications only; clear it when they are read.
- Notification actions: none that only opens the app; prefer nondestructive; short verb label.
- Pre-permission screen: one button that opens the system prompt; no other actions or way to skip it unless needed for legal consent.

## Onboarding and launch
- Launch instantly; restore previous state.
- Launch screen nearly identical to first screen: no text, no branding, no advertising.
- Any splash screen goes at the start of onboarding, not at launch.
- Onboarding brief, interactive, focused on the experience; prefer contextual tips over a long flow.
- Tutorials optional and skippable; not repeated after skip; findable later in help or settings.
- Delay sign-in until needed; explain account benefits; name the exact authentication method on the button.

## Settings
- Sensible defaults for most people; minimize the number of settings.
- Do not ask for what can be detected; respect system-wide settings, no duplicates.
- Make settings reachable in the expected way (menu command or shortcut).
- Task-specific options (filter, sort, show/hide) belong on the screen they affect, not in settings.

## Undo and destructive actions
- Support multiple undo/redo; do not cap it unnecessarily; do not redefine standard gestures.
- Label undo with the action ("Undo Typing"); show or scroll to the result.
- Offer reverting a batch of related changes.
- Prefer undo over confirmation for common actions; confirm only unexpected, irreversible data loss.
- Confirmation: destructive-styled button naming the action, plus Cancel; confirm completion of significant tasks.
- When a command cannot run, say so and why.
