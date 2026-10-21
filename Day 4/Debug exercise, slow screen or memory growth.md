# Debug Exercise: Slow Screen or Memory Growth

The app works correctly, but it's slow:

- Focus movement lags behind the button press.
- Scrolling stutters.
- A screen takes seconds to open.
- The app gets slower the longer you use it, then eventually crashes or is killed by the OS.

## Why TVs Are Harder Than Phones

| Factor | What it means |
|---|---|
| Weak hardware | Many TVs have a slow CPU and GPU and little RAM |
| Big screens | A 4K UI means more pixels, bigger images, and more work per frame |
| Long sessions | People leave TV apps open for hours, so small leaks add up |
| No easy debugging | There's often no DevTools on the device, so you need measurements from outside |

## Classify: Which Kind of Slow?

| Type | Symptom | Likely area |
|---|---|---|
| JS thread slow | Focus effect or `onPress` reacts late, UI freezes while logic runs | Too many re-renders, heavy work in handlers |
| Render/UI slow | Scrolling stutters even though JS is idle | Too many views, huge images, shadows, opacity, animations |
| Slow start | A screen takes long to appear | Loading too much at once, big bundles, many images |
| Memory growth | Fine at first, worse over time, finally crashes | Leaks, images and videos never released |

## Common Causes

| Cause | What it looks like |
|---|---|
| Rendering a long list with `ScrollView` and `.map()` | Every item is mounted, so the screen is slow and memory use is huge |
| Poor `FlatList` setup (no `keyExtractor`, heavy `renderItem`, huge `windowSize`) | Stutter, and memory use grows with list size |
| Re-rendering the whole screen on every focus change | Each key press costs a full re-render |
| Oversized images | High memory use and slow decoding |
| Timers, listeners, and subscriptions not cleaned up | Memory grows every time a screen is opened |
| Players or large resources not released after leaving a screen | Memory never goes back down |

## Tools to Collect Evidence

| Tool | Use |
|---|---|
| Dev menu Perf Monitor | Quick view of JS and UI frame rates |
| React DevTools Profiler | Which components re-render and how long they take |
| Android Studio Profiler | CPU and memory on Android TV |
| Xcode Instruments | CPU and memory on Apple TV |
| Remote DevTools | Profiling on LG and Samsung browsers |

## Optimize Early vs Measure First

| Approach | Pros | Cons |
|---|---|---|
| Optimize early | Avoids many problems, cheap to do at the beginning | Can add complexity you don't need, and can optimize the wrong thing |
| Measure first  | Fixes what actually matters, keeps code simple | Needs a real device and tools, and problems are found late |
