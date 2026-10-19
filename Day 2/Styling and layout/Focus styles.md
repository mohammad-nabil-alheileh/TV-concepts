# Focus Styles

On a TV there is no finger and no mouse. The user moves a **focus** around with the D-pad, and exactly one item is focused at a time.

The focus style is the only way the user knows where they are. If it is missing, weak, or cropped, the app is unusable.

## Five parts of focus

| Part               | What it does                                      |
| ------------------ | ------------------------------------------------- |
| Border             | A ring around the item                            |
| Scale              | The item grows slightly                           |
| Shadow             | Adds depth, so the item looks lifted              |
| Overflow clipping  | The scaled item must not get cut off              |

## 1. Tracking focus

Use `onFocus` and `onBlur` to keep a focus state. Do not depend on `:hover` or pressed styles, because a TV has no pointer.

## 2. Border

Keep the same `borderWidth` at all times, and change only the color:

- **Unfocused:** transparent border.
- **Focused:** visible border color.

If you add a border only when the item is focused, the layout shifts by a few pixels every time focus moves.

## 3. Scale

Scaling the focused item makes it grow. Leave enough space between cards for the growth, so the focused card does not overlap its neighbors.

## 4. Shadow

On weak TV hardware, large blurred shadows are expensive to draw. Apply the shadow to the focused item only.

## 5. Focused vs selected

These two states are easy to confuse. Keep them separate.

| State    | Meaning                          | Lasts                          |
| -------- | -------------------------------- | ------------------------------ |
| Focused  | Where the cursor is right now    | Moves with every D-pad press   |
| Selected | The choice that is active        | Stays until changed            |

Example: in a row of tabs, the focus moves across the tabs as the user presses left and right. The selected tab changes only when the user presses OK.

## Rules

- Keep focus styles visible inside the safe area. A focus ring at the edge of the screen can be cropped by overscan.
- Always scale the focus values with the same scale factor as the rest of the layout.
