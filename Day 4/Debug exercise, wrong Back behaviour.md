# Debug Exercise: Wrong Back Behaviour

The user presses Back and something unexpected happens:

- The app closes when it should go to the previous screen.
- Back does nothing.
- Back closes the wrong layer.
- Back goes back two screens.

## Common Causes of Wrong Behaviour

| Cause | What happens |
|---|---|
| Listener not removed on unmount | A closed screen still reacts to Back |
| Listener registered in the wrong order | The wrong layer handles Back first |
| Handler returns `true` when it shouldn't | Back does nothing |
| Handler forgets to return `true` | Back both closes the popup and leaves the screen |
| Navigation uses `replace` instead of `push` | There's no previous screen to return to, so the app exits |
| Nested navigators | The inner or outer stack handles Back unexpectedly |
| Modal or overlay open | Back should close it first, not the screen behind it |
| Web TVs: Back key not registered | The key never arrives |

## Default Back vs Custom Back Handling

| Approach | Pros | Cons |
|---|---|---|
| Use navigation library defaults | Less code, consistent, usually correct | Doesn't cover popups, custom overlays, or special rules like "double-press to exit" |
| Custom `BackHandler` logic | Full control, handles overlays and confirmation dialogs | Easy to get wrong, so more bugs and more testing |
