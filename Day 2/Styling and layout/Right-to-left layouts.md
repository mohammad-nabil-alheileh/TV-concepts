# Right-to-Left (RTL) Layouts

Languages such as Arabic read from right to left. In an RTL layout, the whole screen mirrors:

- The first item sits on the right.
- Menus open from the right.
- "Forward" points left.

## What flips and what stays the same

| Flips | Stays the same |
| ----- | -------------- |
| Row order | Remote keys |
| Side menu position | Logos and brand marks |
| Text alignment and reading order | Numbers |
| Back and next arrows, chevrons | Most media icons, such as play |
| Slide-in and slide-out directions | Vertical order |
| Start and end padding and margins | The Back button on the remote |

## 1. Use start and end instead of left and right

Use logical properties so the layout flips automatically:

| Use this | Instead of |
| -------- | ---------- |
| `marginStart`, `marginEnd` | `marginLeft`, `marginRight` |
| `paddingStart`, `paddingEnd` | `paddingLeft`, `paddingRight` |
| `borderStartWidth` | `borderLeftWidth` |
| `start`, `end` (positions) | `left`, `right` |

## 2. Focus direction

There are two cases:

| Case | What happens | What to check |
| ---- | ------------ | ------------- |
| Automatic | If the layout is mirrored correctly, pressing Left moves to the item on the left, which is now the next item | Confirm the mirrored layout works with the D-pad |
| Manual | Explicit focus targets override the automatic order | Check `nextFocusLeft` and `nextFocusRight` and swap them for RTL |

## 3. Animations

Direction-based motion must flip. For example, a panel that slides in from the right in LTR should slide in from the left in RTL.

## 4. Icons

| Icon type | Mirror it? |
| --------- | ---------- |
| Directional icons (arrows, chevrons) | Yes |
| Logos | No |
| Numbers | No |
| Clock | No |
| Playback controls and seek bars | Debated. Decide per app and test with users |

## Rules

- Use `start` and `end` for every horizontal spacing and position value.
- Test focus movement with the D-pad in RTL mode, not only the visual layout.
- Mirror directional icons, but not logos, numbers, or clocks.
