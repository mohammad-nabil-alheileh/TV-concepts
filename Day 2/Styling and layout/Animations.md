# Animations

TV hardware is weak. A cheap TV has a slow CPU and GPU, and a 4K screen has four times the pixels of 1080p. Three rules keep animations smooth and safe:

1. Animate only `transform` and `opacity`.
2. Do not use the native driver on web.
3. Never let an animation leave content invisible.

## 1. Animate only transform and opacity

| Property | Examples | Why |
| -------- | -------- | --- |
| `transform` | `scale`, `translateX`, `translateY` | Does not change layout, so neighbors do not move. Cheap on every platform. |
| `opacity` | `0` to `1` | Does not change layout, so neighbors do not move. Cheap on every platform. |

Animating layout properties such as `width`, `height`, `margin`, or `padding` forces the layout to recalculate on every frame. On weak hardware, this causes stutter.

## 2. No native driver on web

The `useNativeDriver` option depends on the platform:

| Platform | `useNativeDriver: true` | Reason |
| -------- | ----------------------- | ------ |
| Android TV | Use it | Moves the animation to the native side, so it keeps running even when the JS thread is busy |
| tvOS | Use it | Same as Android TV |
| Web | Do not use it | No native animated module exists. The animation runs in JavaScript |

On web, `react-native-web` falls back to JavaScript-driven animation. It typically logs a warning if you ask for the native driver.

Because the animation runs on the JS thread on web, a busy thread (for example, a large list rendering) makes the animation drop frames. Keep animations **short and few**.

## 3. Check nothing stays invisible

A common pattern is a fade-in that starts at `opacity: 0`. If the animation never finishes, the content stays invisible forever.

## Rules

- Animate only `transform` and `opacity`.
- Pass `useNativeDriver: true` on Android TV and tvOS, and leave it out on web.
- Keep the number of simultaneous animations low.
- Always end an animation on a visible state.
