# App Suspend and Resume on TV

A TV app does not just run or quit. It can be:

- **Suspended** when the user presses Home, switches apps, or the TV goes to standby or starts a screensaver.
- **Resumed** later, or **killed** by the system to free memory. A killed app starts cold the next time.

## What triggers it, per platform

| Platform | Signal to listen for |
| -------- | -------------------- |
| Android TV, Apple TV | React Native's `AppState` (`active`, `inactive`, `background`) |
| Tizen | `document.visibilitychange` |
| webOS | `document.visibilitychange`, plus the `webOSRelaunch` event when the app is launched again while already running |

## What to do on suspend

| Action | Details |
| ------ | ------- |
| Pause playback and save the position | Keep the user's place in the video |
| Stop timers and network work | Login polling, auto-refresh intervals, websockets |
| Persist state | The current route, the last-focused item, the playback position |
| Do not try to show UI | The user has already left |

## What to do on resume

| Action | Details |
| ------ | ------- |
| Check the session | Refresh the token if it expired while the app was away |
| Check connectivity | Feed the result into the offline state |
| Refresh stale data | Only if the app was away long enough to matter |
| Restore focus | Otherwise the D-pad does nothing |

## Cold start vs resume

The system may kill the app while it is suspended. The next launch is then a **cold start**, and no resume event fires.

Two things follow from this:

1. **Save state continuously**, not only in the suspend handler. A kill can come without warning, and cleanup code such as `useEffect` return functions may never run.
2. **On startup, read the saved state** and decide whether to restore it or start at Home.

## Suspend is not exit

| Event | Result |
| ----- | ------ |
| Home button | Suspend. The app may come back |
| Back from the root screen | Exit, usually with a confirmation overlay |
| Screensaver or standby | Suspend. Many apps get this wrong and keep playing audio |

## Rules

- Stop audio and video when the app is suspended by standby or the screensaver.
- Save state continuously, so a cold start can recover it.
- Restore focus on every resume.
