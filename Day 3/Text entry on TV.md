# Text Entry on TV

Typing with a D-pad is slow and painful. To enter one letter, the user moves the focus to a key and presses OK, then repeats. Typing an email address and password can take over a minute.

The best text entry on TV is the one you avoid. When you cannot avoid it, pick the least painful option.

## Why It Matters on TV

- There is no physical keyboard, and the remote has no letters.
- Sign-in and search are the two flows that need text, and they are the first things users do. A bad experience there loses users before they see your content.
- Every platform has a different keyboard behaviour, so you cannot assume one approach works everywhere.

## Option 1: The On-Screen Keyboard

The system keyboard appears automatically when a `TextInput` takes focus. It is the least work and feels familiar to users.

### Design Tips for a Custom Keyboard

| Tip | Why |
|---|---|
| Put the keys in a simple grid so Up, Down, Left, and Right behave predictably | A QWERTY layout is familiar, but a plain A to Z grid is faster for D-pad users |
| Put Delete, Space, and Submit within easy reach | These are the most-used keys after letters |
| Keep each key's focus state local | Avoids re-rendering the whole keyboard on every press (see [Keep focus state local to the focused item](Keep%20focus%20state%20local%20to%20the%20focused%20item.md)) |
| Support the remote's Back button to close the keyboard, and any physical or Bluetooth keyboard | Users expect Back to dismiss the keyboard, and some connect a keyboard |
| Localise the layouts | An Arabic keyboard needs its own letter set and right-to-left ordering, not just translated labels |

## Option 2: Second-Screen Input

Let the user type on their phone instead. The TV shows a QR code (and a short code as a fallback), the user scans it, signs in or types on the phone, and the TV signs in automatically.

| Detail | What to do |
|---|---|
| Code lifetime | The code must be short-lived and single-use |
| Fallback | Offer a manual code, because some users cannot scan from across the room |
| Polling | Poll gently, and stop polling when the screen unmounts |
| Expiry | Show a clear expiry and a "get a new code" button, with focus on it |
| Last resort | Keep a normal manual sign-in for users without a phone |

## Option 3: Voice Input

Many TV remotes have a microphone button. Voice works well for search and badly for passwords.

| Platform | Voice support |
|---|---|
| Android TV and Apple TV | System speech services provide dictation |
| LG and Samsung | Voice APIs are platform-specific and vary by model and region |

Rules for voice input:

- Treat voice as an extra, never the only way in.
- Request microphone permission only when the user taps the mic, not at startup.
- Handle misrecognition: show the recognised text and let the user edit it.
- Arabic and other languages vary in recognition quality, so test with real speakers.

## Choosing Between Them

| Task | Best option |
|---|---|
| Sign-in | Second-screen (QR), with manual fallback |
| Search | System or custom keyboard, plus voice as an extra |
| Short text (profile name, PIN) | On-screen keyboard |
| Long text (reviews, messages) | Avoid, or move to the phone |
| Passwords | Second-screen; never voice |
