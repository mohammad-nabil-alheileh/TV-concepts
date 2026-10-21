# Measure on the Weakest Real Device with a Release Build

Build in release mode and measure on the slowest device you support.

## Why It Matters on TV

- TV chips are often **5 to 10 times slower** than a phone.
- A development build is not representative. It includes warnings, extra checks, and unoptimised JavaScript. A screen that runs at 15 fps in dev can run fine in release, and the reverse can happen too.
- Emulators and simulators use your computer's CPU and RAM, so they **hide the real problems**.

## Dev Build vs Release Build

| Aspect | Dev build | Release build |
|---|---|---|
| Warnings and dev checks | Included | Stripped |
| JavaScript optimisation | Minimal | Optimised |
| Use it for | Debugging | Measuring performance |

## What to Measure

| Metric | What it means |
|---|---|
| Time to first interactive screen | Time from app launch until the user can act on the first screen |
| Focus latency | Time from a D-pad press to the highlight appearing |
| Frame rate while scrolling a rail | Smoothness of horizontal scrolling |
| Memory use over a long session | Whether memory keeps growing over time |

