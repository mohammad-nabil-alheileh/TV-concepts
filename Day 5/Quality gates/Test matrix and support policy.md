# Test Matrix and Support Policy

| Term | Meaning |
|---|---|
| **Support policy** | A written promise about what you officially support. |
| **Test matrix** | The concrete grid of combinations you actually test, derived from that policy. |

You can't test every combination, so you pick representative ones.

## The Three Dimensions

| Dimension | Examples | Why it matters |
|---|---|---|
| Platform | iOS, Android, (tvOS / Android TV / web) | Different native code, permissions, and navigation behavior |
| OS version | iOS 16/17/18, Android 8 → 15 | Behavior changes between versions |
| Device tier | Low-end, mid, high-end | RAM, CPU, and screen size change performance and layout bugs |

## How to Build One

1. **Use real data.** Check analytics to see which OS versions and devices your users have.
2. **Set the policy.** A common rule: support the last N major OS versions.
3. **Pick matrix rows.** Choose the oldest supported OS, the newest OS, and one in between. Pair them with a low-, mid-, and high-tier device.
