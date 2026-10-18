# LG Magic Remote as a pointer

The LG Magic Remote adds a **second way to interact**. You wave it like a laser pointer, an on-screen cursor follows it, and the scroll wheel scrolls. To your web app, this looks like a mouse.

## Remote actions as browser events

| Remote action | What the browser sees |
|---|---|
| Move the remote | `mousemove`, `mouseenter`, `mouseleave` |
| Press OK on the cursor | `click` |
| Scroll wheel | `wheel` |
| D-pad arrows / OK | `keydown` (Left/Up/Right/Down, Enter) |

The LG app has **two input modes at once**, pointer mode and focus mode, and they can conflict.

## How the modes behave on webOS

- When the user moves the remote, the cursor appears and pointer events fire.
- When the user presses an arrow key, the cursor hides and you're back in focus mode.
- The cursor also hides after a few seconds of inactivity.

## Example 1: hover should move focus

Without this, hovering highlights nothing in your focus system, and clicking a card that was never focused can behave oddly.

```jsx
const { ref, focused, focusSelf } = useFocusable({ onEnterPress: onSelect });

return (
  <div
    ref={ref}
    onMouseEnter={focusSelf}   // pointer enters → card becomes the focused card
    onClick={onSelect}         // pointer click → same action as OK
    style={{ outline: focused ? '4px solid white' : 'none' }}
  >
    {title}
  </div>
);
```

## Example 2: the classic bug and its fix

**The bug:** The user scrolls a row with the arrow keys while the cursor is parked somewhere on screen. Content slides under the stationary cursor, the browser fires `mouseenter` on whatever is now underneath, and focus jumps away from where the user was navigating.

**The fix:** Only react to a mouse that really moved.

```js
let pointerActive = false;
document.addEventListener('mousemove', () => { pointerActive = true; });
document.addEventListener('keydown',   () => { pointerActive = false; });
```
