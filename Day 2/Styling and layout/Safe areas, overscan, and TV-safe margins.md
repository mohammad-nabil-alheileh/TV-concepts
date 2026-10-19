# Safe Areas, Overscan, and TV-Safe Margins

## What is overscan

Some TVs do not show the whole picture your app draws. This is called **overscan**: the TV crops or zooms the image slightly, so pixels at the very edge of the screen are cut off.

Because of this, you cannot place content right up to the edges. The fix is a **safe area**: a margin around the screen where you keep everything the user must see or interact with.

## Two zones

| Zone                | What goes there                                              | Typical size       |
| ------------------- | ------------------------------------------------------------ | ------------------ |
| Safe area (inner)   | Text, buttons, cards, focus rings, anything interactive      | About 5% inset on each side |
| Bleed (outer edge)  | Background images, gradients, video, color fills             | Full screen        |

## Safe area size at 1920x1080

The 5% inset is measured from the reference design size from the scaling topic:

| Edge        | 5% of the design size | Safe area in 1920x1080 |
| ----------- | --------------------- | ---------------------- |
| Left / right | 5% of 1920 = 96 px   | Content from x = 96 to x = 1824 |
| Top / bottom | 5% of 1080 = 54 px   | Content from y = 54 to y = 1026 |

Use these values in the 1920 design space and scale them with the same scale factor as the rest of the layout.

## Example

The screen draws the background across the full screen and places all real content inside the safe area:

```tsx
function Screen({ children }: { children: React.ReactNode }) {
  const s = useScale(); // scale helper from the scaling topic

  return (
    <View style={{ flex: 1 }}>
      {/* Bleed: fills the whole screen, may be cropped by overscan */}
      <Image
        source={require('./hero-bg.jpg')}
        style={StyleSheet.absoluteFill}
        resizeMode="cover"
      />

      {/* Safe area: all real content lives here */}
      <View
        style={{
          flex: 1,
          paddingHorizontal: s(96),
          paddingVertical: s(54),
        }}
      >
        {children}
      </View>
    </View>
  );
}
```

## Rules

- Put backgrounds, gradients, and video in the bleed zone, so they fill the screen edge to edge.
- Put text, buttons, cards, and focus rings inside the safe area only.
- Never let a focus ring or highlight touch the screen edge. Cropping would hide it.
- Apply the padding in the 1920 design space and scale it, so the margin stays 5% on every resolution.
