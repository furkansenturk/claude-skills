# App patterns

## Contents
- [Accounts](#accounts)
- [Offering help](#offering-help)
- [Ratings and reviews](#ratings-and-reviews)
- [Sharing and collaboration](#sharing-and-collaboration)
- [File management](#file-management)
- [Windows, full screen, multitasking](#windows-full-screen-multitasking)
- [Audio](#audio)
- [Video](#video)
- [Charts and data visualization](#charts-and-data-visualization)
- [Branding](#branding)
- [AI features](#ai-features)
- [Purchases and subscriptions](#purchases-and-subscriptions)
- [Sync, offline, web content](#sync-offline-web-content)

## Accounts
- Require an account only if core functionality needs it; otherwise let people use the app without one.
- Delay sign-in as long as possible: let people explore first; require it only at the point of commitment (e.g. checkout).
- On the sign-in view, briefly state why an account is needed and its benefits.
- Prefer a federated sign-in or passkeys over passwords. Support credential autofill.
- Label sign-in buttons with the exact method ("Sign In with <method>"), not a generic "Sign In". Mention only methods available in the current context.
- No in-app opt-in setting for biometric authentication; it is a system-level choice.
- Never call account authentication a "passcode".
- If accounts can be created in-app, provide in-app account deletion (not just deactivation). If not possible in-app, link directly to the deletion page; make it easy to find, not buried in privacy policy or terms.
- Same deletion experience in app and on web; neither longer or more complicated.
- State when deletion will complete and notify when finished.
- If purchases or subscriptions exist, explain how billing and cancellation work after deletion and how to cancel.

## Offering help
- Match help to task: inline description for one- or two-step tasks; tutorial for complex multistep tasks.
- Do not explain standard components. Explain only app-specific actions or unconventional controls (prefer animation).
- Tip: small transient view for a new or less obvious feature. Only for features of three actions or fewer.
- Tip text: one or two sentences, direct and action-oriented, no promotional content.
- Popover tip preserves content flow; inline tip keeps surrounding content visible. Annotation style points to a specific element; hint style is not tied to one.
- Show a tip only to people who might benefit: rules based on parameters or events; never for features already used. With multiple tips, control ordering and frequency.
- Tooltip (pointer or gaze hover): describe only the hovered control; start with a verb ("Restore default settings"); do not repeat the control's name.
- Tooltip length 60 to 75 characters maximum; sentence fragment, sentence case, no ending period. May vary by control state.

## Ratings and reviews
- Prefer the system-provided rating prompt.
- Ask only after demonstrated engagement (completed level or significant task, number of launches, features explored). Never on first launch or during onboarding.
- Never interrupt a task or gameplay; ask at natural breaks.
- Leave at least a week or two between requests; ask again only after further engagement.

## Sharing and collaboration
- Put the Share button in a convenient place such as the toolbar. Use the system share interface.
- Summarize permissions in a succinct phrase ("Only invited people can edit", "Everyone can make changes").
- Show the collaboration control prominently as soon as collaboration starts; it signals shared content and who shares it.
- Consider notifying on collaboration events (content change, membership change, mention) with a deep link to the relevant view.

## File management
- Provide New and Open via menus and keyboard shortcuts.
- Use the system file browser; custom browsers must match people's understanding of the file system.
- Custom open UI: include open recent, filtering, multiple selection.
- Autosave periodically while editing, on close, and on switching away. No explicit save required; work is preserved unless canceled or deleted.
- Save UI lets people change name, format, location; default new document title "Untitled"; default to a logical location. Accessory options allowed in the save dialog.
- Hide file extensions by default, let people show them, and reflect the choice in all open and save interfaces.
- If autosave can be off: show unsaved changes (dot on the close button and in the window list), and prompt to save on close or quit. Never show the dot when autosave is on.

## Windows, full screen, multitasking
- Windows adapt fluidly to any size; set sensible minimum and maximum sizes. Restore size and placement.
- Open a new window only when it helps multitasking or preserves context (e.g. compose). Offer "open in new window" as an option, not default.
- Use system window frames and controls; no custom window chrome.
- Full screen: support it for games, media, and in-depth tasks. Use the system full-screen mode. People choose when to enter and exit; never end it automatically.
- In full screen, adjust layout to the space but never resize the window programmatically. Keep essential controls available or easy to reveal.
- Defer system gestures in full-screen games to prevent accidental exits.
- Always be ready to save and restore context; people may multitask at any time.
- On switching away: pause attention-requiring activity (games, media) and resume seamlessly on return.
- Finish user-initiated tasks (downloads, processing) in the background. Notify on completion of important or time-sensitive tasks; otherwise use notifications sparingly.
- Do not pause a window's video playback when focus moves to another window.
- Hide system bars only temporarily (full-screen media); a simple gesture brings them back.

## Audio
- Follow system volume and silent mode. Adjust only relative levels within the app, never overall volume.
- Allow rerouting of output; use the system volume control.
- Choose the audio category by role: nonessential and silencing others; nonessential and mixing; essential and may play in background; record; play and record.
- Primary interruptions (music, podcasts, audiobooks): pause indefinitely. Short interruptions (navigation prompts): lower volume or pause, then restore on end.
- Resume automatically after resumable interruptions (e.g. phone call); not after nonresumable ones (e.g. another app starting playlist).
- When your temporary audio ends, signal other apps they may resume.
- Respond to external controls (headphones, system media controls) only when it makes sense; never redefine their meaning; ignore unsupported ones.
- Never convey important information by sound alone.

## Video
- Use the system video player. Show video at its original aspect ratio; no embedded letterbox or pillarbox padding.
- Wide video (2:1 through 2.40:1) defaults to fill (edges may crop); other aspect ratios default to fit.
- Provide captions, subtitles, and audio-language selection.
- Support picture-in-picture where available. Space toggles play and pause.
- Resume playback automatically from the previous end time; never ask whether to resume.
- Start playback immediately, with no splash, detail, or intro screens. Avoid loading screens; if loading exceeds two seconds, show a black screen with a centered spinner and minimal branding, only until playback can begin.
- Let people choose when to start playback. Never auto-start fully immersive video.

## Charts and data visualization
- Use a chart only to highlight important information. For plain data to scroll, search, or sort, use a list or table.
- Keep charts simple; reveal details on demand. Never require interaction to see critical information.
- Prefer common types: bar to compare categories or parts of a whole; line for change over time and trends; point for relationships, outliers, clusters. Combine types (line plus points) when it adds clarity. Teach novel chart types.
- Add title, subtitle, annotations, and a summary of the main message. Descriptions explain the chart's purpose before viewing.
- Axis: fixed range when bounds carry meaning; dynamic range when values vary widely. Bar charts start at zero. Use familiar tick sequences (0, 5, 10). Use enough grid lines to estimate values, not so many they overwhelm.
- Consistency across charts: same type, colors, annotations, layout, descriptive text for the same data. Deviate only to highlight differences.
- Size the chart for its detail and interactivity. Make small marks easy to target (larger hit areas). Support keyboard and switch navigation in a logical sequence.
- Never rely on color alone: add labels, patterns, or shapes. Separate adjacent colored areas (e.g. stacked bars) with separators.
- Accessibility: a title and summary for the whole chart, plus a label per important or interactive mark.
- Labels: include context (date, place) with the value; use actual values, not subjective words (rapidly, gradually); avoid ambiguous formats ("June 6" not "6/6", "60 minutes" not "60m"); describe what series represent, not their colors; name axes in a consistent order.
- Compact width: maximize plot width, shorten vertical-axis labels.
- Hide visible axis and tick labels from assistive tech; expose mark values through accessibility labels.

## Branding
- Express brand within system conventions: voice and tone in copy, standard components lightly customized, optional custom font for headlines only, system fonts for body.
- Use the accent color judiciously: primary actions and status indicators (unread badge, selected tab icon). Minimize it on controls.
- Branding defers to content. No logo scattered through the app unless essential for context.
- Do not use the launch screen for branding.

## AI features
- Say where the app uses AI; never present generated content as written by a person.
- Put Edit, Undo, Retry or Adjust next to generated results; confirm when a correction takes effect.
- Ask before any irreversible or risky action (delete, purchase); never automate it.
- Warn that generated content can be wrong; keep the experience usable when AI is off or unavailable.
- Feedback on suggestions is always optional; apply it immediately.

## Purchases and subscriptions
- Show the total billing price of every purchase, with billing period and any price after an introductory offer.
- Make cancelling a subscription easy to find.

## Sync, offline, web content
- When sync is unavailable, keep working locally; no alert just to say sync is off.
- In-app web view: offer back and forward when people can visit several pages.
