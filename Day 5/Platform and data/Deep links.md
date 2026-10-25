# Deep Links

A deep link is a URL that opens your app directly on a specific screen, for example `myapp://product/42` or `https://myapp.com/product/42`. It can come from a notification, an email, a QR code, a web page, or another app.

## Link Types

| Type | Example | Notes |
|---|---|---|
| Custom scheme | `myapp://product/42` | Easy to set up, but any app can claim the same scheme, and it fails if the app isn't installed |
| Universal Links (iOS) / App Links (Android) | `https://myapp.com/product/42` | Verified by your domain, so no hijacking; falls back to the website if the app isn't installed |

## The Four Cases

### a) Cold Start

The app was not running. The OS launches it with the URL, and your JS bundle has to boot first. The URL is available through `Linking.getInitialURL()`, and React Navigation's `linking` prop reads it for you.

**What can go wrong:**

- Showing the splash screen until navigation is ready, or the link appears to do nothing.
- Fetching the data the target screen needs only after it mounts, so the user lands on an empty screen.

### b) Running App (Foreground or Background)

The app is already alive. The OS delivers the URL as an event, and the navigation state must change without resetting what the user is doing.

**What can go wrong:**

- Navigating to the same screen with new params: it should update params instead of pushing a new screen.
- Interrupting something important, such as a payment or an unsaved form.

### c) Login Required

The link points to protected content, but the user isn't signed in. Don't drop the link. Save it, send the user to login, then continue to the target after success.

**What can go wrong:**

- Losing the link after login, so the user ends up on Home and wonders what happened.
- Keeping the pending link forever. Clear it on logout and expire it after a timeout.
- A link that arrives while the session is expired or the token is being refreshed.

### d) Back Stack

The user opens `myapp://product/42` and presses back. What should happen? If Product is the only screen in the stack, back exits the app, which feels broken. Usually they should go back to a sensible parent screen.
