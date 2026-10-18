# Testing the web build in Chrome, then on the real TV

Test in **two stages**, because each catches different bugs.

## Two stages compared

| Stage | Strength | Limitation |
|---|---|---|
| **1. Chrome on your desktop** | Fast, with full DevTools. Proves your focus logic and key handling work. | Can't tell you whether the app works on a TV. |
| **2. The real TV** | The only place you'll find performance, rendering, and remote-specific problems. | Slow to iterate on. |

> Chrome can't tell you whether the app works on a TV. It can only tell you whether your logic is correct.

## Stage 1: Chrome with the keyboard as a fake remote

| Remote button | Chrome key | What your app does |
|---|---|---|
| D-pad | Arrow keys | Spatial navigation moves focus |
| OK / Select | Enter | `onEnterPress` fires |
| Back | Backspace | Go back / close modal |

### What to check in Chrome

- [ ] Every screen is reachable with arrows alone, with no mouse.
- [ ] Focus is always visible (you can always tell which item is selected).
- [ ] No focus traps.
- [ ] Returning to a row restores the last card.
- [ ] At the TV viewport (1920×1080 or 1280×720), text and targets are readable from a distance.

## Stage 2: The real TV

### Typical workflow

1. Build the web bundle.
2. Package it and install it on the TV, with the TV in Developer Mode.
3. Debug remotely with `ares-inspect`, which opens DevTools connected to the TV.

### What only the real TV reveals

| Area | What to look for |
|---|---|
| **Old browser engines** | Older TVs ship old Chromium versions, so modern JS or CSS features may be missing. |
| **Back-button behavior** | The real key code, and what the platform does if you don't handle it. |
| **Magic Remote pointer** | Pointer behavior on the real remote. |
| **Performance** | Low-end TV CPUs make animations and big lists stutter even when Chrome runs them smoothly. |
| **Safe area, overscan, and colors** | Whether edges are cropped, and how colors look on the panel. |
| **Text legibility** | Whether text is readable from 3 m away. |
| **Scroll wheel and cursor** | Cursor hide/show behavior and scroll wheel response. |
