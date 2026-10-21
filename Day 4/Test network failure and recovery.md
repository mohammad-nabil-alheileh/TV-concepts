# Test Network Failure and Recovery

A TV app depends on the network for catalogs, images, streams, and login. TV networks are often poor: weak Wi-Fi, a router far from the living room, or a TV waking from standby before the connection is back. So you test what the app does when the network fails, and what it does when the network comes back.

## Kinds of Network Failure

| Failure | Example | What users see if you don't handle it |
|---|---|---|
| Offline at launch | The TV starts with no connection | A blank screen or an endless spinner |
| Drops mid-use | Wi-Fi disconnects while browsing | Rows stop loading, and actions silently fail |
| Slow network | Very low bandwidth, high latency | Spinners for a long time, or timeouts |
| Timeout | The server never answers | The app waits forever |
| Server error | HTTP 500 or 503 | A crash, or a generic broken screen |
| Partial failure | Rows load, but one request fails | A half-empty screen with no explanation |
| Recovery | The network comes back | The app stays stuck on the error and needs a restart |

## What the App Should Do

1. **Show a clear state.** Loading, error, and empty are three different states, so don't show them all as a blank screen.
2. **Offer a way to retry** with a focusable button, since there is no touch.
3. **Move focus to that button** so the user can press Select right away. If focus is lost, the user is trapped on the error screen.
4. **Make Back work** so the user can always leave the error screen.
5. **Recover automatically when possible.** When the connection returns, retry on its own, or refresh when the screen regains focus.
6. **Set timeouts** so a hung request becomes an error instead of waiting forever.
7. **Keep what you already have.** If cached content exists, show it instead of an error.

## How to Test It

| Method | How | Good for |
|---|---|---|
| Disconnect | Turn off Wi-Fi or unplug Ethernet | Offline at launch, drop mid-use, recovery |
| Throttle | Chrome DevTools network throttling | Slow network, timeouts |
| Proxy tool | Charles, mitmproxy, or similar, to delay, block, or modify requests | Specific failures: one endpoint failing, slow images |
| Mock server | A local server that returns 500, 503, empty bodies, or hangs on purpose | Server errors, partial failures |
| Component tests | Mock `fetch` to reject, then check the error state and Retry button | Your error-handling logic |
| Smoke test routine | Add a "network off, then on" sequence to your list | The real behaviour on a device |
