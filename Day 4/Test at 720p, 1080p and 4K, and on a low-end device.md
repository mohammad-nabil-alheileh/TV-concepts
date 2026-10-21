# Test at 720p, 1080p, and 4K, and on a Low-End Device

The same app runs on very different TVs. A layout or speed that looks fine on your development setup can break on a smaller screen, a sharper one, or a weaker chip.

## Two Separate Things to Vary

| Variable | What changes | Typical problems |
|---|---|---|
| Resolution and density (720p, 1080p, 4K) | How much space you have, and how sharp things are | Overflow, clipped content, tiny or huge text, blurry images, wrong spacing |
| Hardware strength (high-end vs low-end) | CPU, GPU, and RAM available | Laggy focus, stuttering scroll, slow start, crashes from memory |

## What Tends to Break at Each Resolution

| Resolution | What to watch for |
|---|---|
| 720p | Content that fits at 1080p now overflows or gets cramped. Text may be too small to read from a distance. Fewer items fit per row |
| 1080p | Your reference point. Most designs are made for this |
| 4K | Low-resolution images look blurry. Big images use much more memory and decode time. Fixed-pixel layouts can look tiny. Everything costs more to draw |

## How to Test Different Resolutions

| Method | Where | Notes |
|---|---|---|
| Emulator profiles | Android TV emulator images in 720p, 1080p, and 4K | Easy to switch, but not a real TV |
| Override size and density with `adb` | Real or emulated Android TV | Useful for a quick check without extra devices |
| Resize the browser window | Web builds | Quick for layout, but doesn't show engine or performance differences |
| Real TVs | Any | The only true test of overscan, density, and speed |

## How to Test a Low-End Device

1. **Use a genuinely weak device.** Try a budget Android TV stick or an old TV model, ideally with around 1 to 2 GB of RAM. An emulator on a fast PC will not show real slowness.
2. **Measure real numbers:**

   | Metric | How to check |
   |---|---|
   | Cold start time | Time from launch to first usable screen |
   | Focus response | Time from key press to visible focus change |
   | Scrolling in the longest list | Smoothness while holding a direction key |
   | Memory after 10 to 20 minutes of normal use | Memory reading at the start and at the end of the session |

3. **Test the worst case, not the average.** Use the heaviest screen, the longest list, and the biggest images.
