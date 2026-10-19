# One Set of States

Every screen that loads data is always in exactly one of these five states:

| State | Meaning |
| ----- | ------- |
| Loading | The request is in flight |
| Success | There is data to show |
| Empty | The request worked, but there is nothing to show |
| Error | The request failed |
| Offline | The device has no connection, so a retry will fail until it comes back |

## Why TV makes this harder than mobile

On a phone, an error screen can be a message plus a tap target. On TV, focus is the problem:

- If the screen shows only text, no element can receive focus.
- The D-pad does nothing.
- The user is stuck on a dead screen with no way to retry.
- Back may be their only way out.

So every state needs either a **focusable action** or a **clear, defined Back behavior**.

## What each state shows

| State | What to show | Focusable action |
| ----- | ------------ | ---------------- |
| Loading | Spinner or skeleton | None. Keep focus somewhere safe, such as the sidebar. Add a timeout that leads to Error |
| Empty | Short message | A useful action, such as "Browse movies". Not a retry |
| Error | Message | Retry. Retry gets initial focus |
| Offline | "No connection" message | Retry, plus auto-retry when the connection returns |

## Rules

- Every state must have a focusable action or a defined Back behavior.
- Loading must time out into Error, so the user is never stuck on a spinner.
- Give the Retry button initial focus on the Error screen.
