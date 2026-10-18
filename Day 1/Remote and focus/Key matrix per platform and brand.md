# Key matrix per platform and brand

Each TV platform sends different events for the same physical button. This note covers what those events contain.

You can't assume "Back is key X." Each platform sends its own codes or event names, and some keys never reach your app at all.

**The practical solution is a key matrix:** a table of what each button sends on each platform, plus a small layer that translates everything into your own action names (`'back'`, `'select'`, `'playPause'`).

## The matrix (main buttons)

| Action | Android TV / Google TV | Apple TV (tvOS) | LG webOS | Samsung Tizen |
|---|---|---|---|---|
| **Arrows** | up/down/left/right events (D-pad key codes 19–22) | up/down/left/right events (swipes on the touch surface) | keyCode 37–40 | keyCode 37–40 |
| **Select / OK** | `select` (key code 23 or 66) | `select` | keyCode 13 | keyCode 13 |
| **Back** | key code 4, via `BackHandler` | `menu` event | keyCode 461 | keyCode 10009 |
| **Play/Pause** | `playPause` (85) | `playPause` | Play 415 and Pause 19 (separate keys) | Play 415 and Pause 19 (separate keys) |
| **Rewind / Fast-forward** | `rewind` / `fastForward` (89 / 90) | Usually swipes or the touch surface | 412 / 417 | 412 / 417 |
| **Color keys** (red, green, yellow, blue) | Usually absent | None | 403–406 | 403–406 |

## Keys your app can't use

Some buttons never reach your app, or must not be overridden:

- **Home / TV button / Exit:** Returns to the launcher on every platform. You cannot intercept it.
- **Apple TV Menu at the root screen:** The system expects it to exit to the Home Screen. If you trap it, you break platform rules and users' expectations.
- **Voice, Settings, and app-shortcut buttons:** Handled by the OS or the manufacturer.
