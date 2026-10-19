# Keep Mounted vs Unmount

When the user navigates away from a screen, you choose between two options.

| Option | What happens | Coming back |
| ------ | ------------ | ----------- |
| Unmount | The screen's component tree is destroyed. Its state, scroll position, focus, and loaded images are gone | Rebuilds the screen from scratch |
| Keep mounted | The screen stays alive in the background, hidden and not rendered to the user | Instant. Everything is exactly as it was |

## What each choice costs

| Option | Cost | Details |
| ------ | ---- | ------- |
| Unmount | CPU and time on return | Re-fetching or re-reading data, re-rendering long lists, and losing scroll and focus position |
| Keep mounted | Memory | Every hidden screen still holds its views, images, timers, listeners, and state |

On a TV with limited memory, keeping many screens mounted can cause the app to slow down or crash. Keep mounted only for screens the user returns to often.

## Focus: the hidden danger

Focus behaves differently in each case, and each one has a trap.

| Case | Problem | Fix |
| ---- | ------- | --- |
| Kept mounted and hidden | If the hidden screen's focusable elements are still focusable, the D-pad can move focus onto something the user cannot see | Make hidden screens non-focusable, not just invisible |
| Unmounted | When the user returns, no element has focus until you set one | Restore focus explicitly when the screen opens |

## Rules

- Hidden screens must be **non-focusable**, not just invisible.
- When you unmount a screen, restore focus when it comes back.
- Keep mounted only the screens that users return to often, and watch memory use.
