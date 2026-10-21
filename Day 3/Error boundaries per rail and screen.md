# Error Boundaries per Rail and Screen

An error boundary is a component that catches errors thrown while rendering its children and shows a fallback instead.

Without one, a single thrown error in any component unmounts the whole app tree, which in a release build means a white screen or a crash. With boundaries placed deliberately, a failure stays contained to the part that broke.

## Why It Matters on TV

- **There is no touch fallback.** A phone user can tap elsewhere; a TV user is stuck on whatever the D-pad can reach. A broken screen with no focusable element means the user must force-quit the app with the remote.
- **Content is messy.** One bad catalogue item should not take down the whole home screen.
- **TV apps run for hours**, so rare errors will eventually happen.

## Two Levels of Boundary

| Level | Catches | Fallback |
|---|---|---|
| Per rail | A bad item or failed rail render | The rail shows an inline "couldn't load, retry" row; the rest of the screen works |
| Per screen | Anything the rails did not catch | A full-screen error with Retry and Back buttons |

## TV-Specific Details

| Rule | Why |
|---|---|
| Always give the fallback a focus target. Use `hasTVPreferredFocus` on the Retry button. | Otherwise the remote will appear dead. |
| Make sure Back still works. The fallback must not swallow the Back button. | Otherwise the user cannot leave the screen. |
| Don't retry forever. Count retries and offer Back after two or three failures. | Repeated retries leave the user stuck in a loop. |
