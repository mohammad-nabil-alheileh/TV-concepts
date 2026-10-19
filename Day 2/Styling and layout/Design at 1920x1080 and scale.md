# Designing at 1920x1080 and Scaling

## The problem

TVs come in several resolutions:

| Resolution | Pixels    | Aspect ratio |
| ---------- | --------- | ------------ |
| 720p       | 1280 x 720  | 16:9       |
| 1080p      | 1920 x 1080 | 16:9       |
| 4K         | 3840 x 2160 | 16:9       |

All of them share the same 16:9 shape. Only the pixel count changes. Writing a separate layout for each size is wasteful, so the approach is:

1. Pick one **reference size**: 1920 x 1080.
2. Design every screen in that 1920 x 1080 space.
3. Scale the numbers at runtime to match the actual screen.

## Why hardcoded pixels break

If a card is 320 px wide in the 1920 design, it covers one sixth of the screen. On a 4K screen it must still cover one sixth of the screen, which means it must become 640 px.

If you hardcode 320, the card stays 320 px on a 3840 px wide screen. It shrinks to a small tile.

## Scale factor

The scale factor compares the width the system reports to the reference width:

```
scale factor = reported screen width / 1920
```

| Screen                     | Width reported | Scale factor |
| -------------------------- | -------------- | ------------ |
| 1080p, 1920 wide           | 1920           | 1.0          |
| 720p, 1280 wide            | 1280           | 0.667        |
| 4K, 3840 wide              | 3840           | 2.0          |
| Android TV 1080p, 960 dp   | 960            | 0.5          |

The Android TV row reports density-independent pixels (dp). The screen is still 1080p, but the system reports a width of 960 dp, so the factor is 0.5.

## Applying the factor

Multiply every design value by the scale factor before drawing it.

| Design value (1920 space) | 720p (x0.667) | 1080p (x1.0) | 4K (x2.0) | Android TV (x0.5) |
| ------------------------- | ------------- | ------------ | --------- | ----------------- |
| 320 px card width         | 213 px        | 320 px       | 640 px    | 160 px            |
| 100 px margin             | 67 px         | 100 px       | 200 px    | 50 px             |

The card keeps the same share of the screen on every device.

## Rules

- Never hardcode pixel values in layout code. Store values in the 1920 x 1080 design space and scale them.
- Use the same scale factor for sizes, margins, font sizes, and spacing so the layout stays proportional.
- Test on at least one smaller and one larger resolution, such as 720p and 4K, before you finish a screen.
