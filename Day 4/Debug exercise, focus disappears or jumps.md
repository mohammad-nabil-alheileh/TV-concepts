# Debug Exercise: Focus Disappears or Jumps

The key arrives, but focus ends up somewhere wrong. There are two ways this happens:

- **Jumps:** focus goes to an unexpected element.
- **Disappears:** no element looks selected, so the next key press does nothing.

## Why Focus Disappears

| Cause | What happens |
|---|---|
| The focused element is unmounted or hidden | Focus has nowhere to stay, so it's lost |
| Nothing has preferred focus when a screen opens | No element starts focused, so the first key press does nothing |
| A modal or overlay closes | Focus isn't restored to where it was |
| The only focusable element in that direction is off-screen or clipped | The engine can't reach it |

## Why Focus Jumps

| Cause | What happens |
|---|---|
| Uneven layout | The engine picks the geometrically "closest" element, not the one you expect |
| A gap between sections with nothing focusable in it | Focus skips over the gap to the next closest element |
| Re-render replaces elements with new keys | Focus resets to the first element |
| An invisible but focusable element sits in the path | Focus lands on something the user can't see |

## Letting the Engine Decide vs Controlling Focus Yourself

| Approach | Pros | Cons |
|---|---|---|
| Trust the engine | Little code, behaves like native TV apps, adapts to layout changes | Unpredictable when layouts are uneven |
| Control it yourself | Predictable, exact paths | More code, can break when the layout changes, and wrong overrides can create traps where focus can't leave |
