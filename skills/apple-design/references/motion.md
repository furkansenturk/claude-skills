# Motion and feedback

## When to animate
- Add motion only with purpose; support the experience, never overshadow it
- Avoid gratuitous or excessive animation
- Avoid motion on frequent UI interactions, especially custom elements
- Never use motion as the only way to convey important information; add haptics or audio
- Standard components already animate; reuse them

## Feedback animation
- Keep feedback animation brief and precise
- Make motion realistic and consistent with gestures and expectations
- Dismiss in the reverse direction of presentation (slid down from top: do not dismiss sideways)
- Let people cancel or skip motion; never block input until an animation completes, especially if repeated
- Use motion that tracks the gesture directly
- Match haptic intensity and sharpness to the animation it accompanies

## Reduce Motion
- Honor the system Reduce Motion setting
- Reduce automatic and repetitive animations: zooming, scaling, peripheral motion
- Tighten springs to reduce bounce
- Track animations directly with gestures
- Replace sliding and zooming transitions with fades
- Do not animate into or out of blurs

## Flashing and comfort
- Be cautious with fast-moving and blinking animations; excess causes distraction, dizziness, epileptic episodes
- Respect the system dim-flashing-lights setting in video playback

## Loading
- Show something as soon as possible; use placeholders replaced as content arrives
- Blank screens read as errors
- Load in the background; keep other actions available
- For unavoidably long loads, show tips or hints; estimate remaining time accurately
- Download large assets in the background
- Content ideally displays instantly; use a progress indicator when loading takes more than a moment or two
- Loading ideally finishes before people notice

## Progress indicators
- Determinate when duration is known; indeterminate when unknown
- Prefer determinate
- Report progress accurately and at an even pace; avoid 90 percent in five seconds then the last 10 percent in 5 minutes
- Keep indicators moving; a stationary one reads as frozen
- If a process stalls, explain the problem and what people can do
- Switch indeterminate to determinate once duration is known
- Never switch spinner to bar or bar to spinner
- Add a description that is accurate and succinct; avoid vague terms like "loading" or "authenticating"
- Show the indicator in a consistent location
- Remove the indicator when the operation completes
- Offer Cancel when halting is safe; add Pause when halting has side effects (such as losing a partial download)
- Alert before cancellation that loses progress, with confirm or resume options
- Pull-to-refresh: hidden by default, revealed on drag down; also refresh content automatically

## Action feedback
- Match the significance of feedback to its delivery: passive for status, interrupting for data-loss warnings
- Convey feedback through several channels: color, text, sound, haptics
- Place status feedback near the items it describes
- Alerts only for critical, ideally actionable information; do not overuse
- Warn before unexpected, irreversible data loss; do not warn when loss is the expected result
- Confirm completion only for significant tasks; people expect success and mainly need to know about failure
- When a command cannot be carried out, say so and explain why

## Haptics
- Use system haptic patterns only for their documented meanings
- Use haptics consistently with a clear cause-and-effect link to the action
- Complement visual and audio feedback; keep all in harmony
- Do not overuse; best haptics go unnoticed but are missed when off
- Prefer short haptics for discrete events; avoid long-running haptics outside gameplay
- Make haptics optional: allow turning off or muting; the app must work without them
- Do not let haptics disrupt camera, gyroscope, or microphone use
- Notification haptics: outcome of a task (success, warning, error)
- Impact haptics: physical metaphor, such as a view snapping into place or a collision (light, medium, heavy, rigid, soft)
- Selection haptics: while values change, such as pickers
- Custom haptics: transient (brief taps) or continuous (sustained), with adjustable sharpness and intensity
