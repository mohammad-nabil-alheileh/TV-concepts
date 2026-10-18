# Hardware limits

TVs in general, and especially cheap streaming sticks and older TVs, have hardware limits.

## The limits

| Limit | What it means | Effect on the app |
|---|---|---|
| **Slow CPUs** | JavaScript runs slower. | Heavy logic or big re-renders cause stutter and laggy focus movement. |
| **Low RAM** | Many devices have only 1–2 GB, shared with the OS and other apps. | If the app uses too much, the system kills it. |
| **Old OS versions** | TVs get few updates, so users stay on old versions for years. | Newer APIs and language features may be missing. |

**Why lag matters more on TV:** If the focus highlight lags behind a button press, the app feels broken. Focus is the only feedback the user gets.

## Solutions

### Slow CPU: keep rendering cheap

- Render only what's needed, and avoid re-rendering rows.
- **Example:** A long list that renders everything at once will freeze a weak CPU.

### Low RAM: shrink images and free what you don't need

| Technique | Example |
|---|---|
| **Shrink images** | Images are usually the biggest memory cost. A 4000×3000 poster shown at 300×450 still gets decoded at full size. Resize images to the size they're displayed at. |
| **Free what you don't need** | Don't keep every screen's data in memory. Unmount offscreen screens. |

### Old OS: check before using new features

- Check that an API or feature exists before using it.
- Pick the minimum supported OS, and build for that.
