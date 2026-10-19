# Screen Readers and Focus Order

A screen reader speaks what is on screen for users who are blind or have low vision. On a TV, it works together with the D-pad: the user moves focus, and the screen reader reads the focused item aloud.

Two things decide whether your app is usable without seeing it:

1. What each focusable item says.
2. The order in which focus moves through the screen.

## 1. What each item says

An image-only poster card has no text. A screen reader says nothing useful, or just "button". Give every focusable item a **label**, a **role**, and a **state**.

```tsx
<Pressable
  accessible
  accessibilityRole="button"
  accessibilityLabel="Dune, 2021, rated PG-13, 2 hours 35 minutes"
  accessibilityState={{ selected: isSelected }}
  onFocus={() => setFocused(true)}
  onBlur={() => setFocused(false)}
>
  <Image source={poster} />
</Pressable>
```

| Property | What it means | Example |
| -------- | ------------- | ------- |
| Label | What the item is, in a sentence a person would say | "Dune, 2021, rated PG-13, 2 hours 35 minutes" |
| Role | What the item does | `button`, `tab`, `header`, `link`, `image` |
| State | Whether the item is selected, checked, or disabled | `selected: isSelected` |

**Label tip:** Put the most important word first. Users often skip ahead, so the title should come before the details.

## 2. Focus order

Focus order is the path focus takes when the user presses the D-pad. It should match what a sighted user expects: **left to right, top to bottom**.

### Initial focus

When a screen opens, put focus somewhere useful. Usually this is the first main item or the primary button.

### Modals and overlays

| Rule | Why |
| ---- | --- |
| Trap focus inside an open dialog | Stops Down from moving into the screen behind the dialog |
| Restore focus to the item that opened the dialog when it closes | Without this, focus is lost and the remote seems dead |
| Never remove or hide the focused element without moving focus first | A removed element leaves focus nowhere to go |

## 3. Announcing changes

When content changes without focus moving, a screen reader user hears nothing unless you announce the change. Examples include a "Added to favorites" message or a loading result.

## Rules

- Give every focusable item a label, a role, and a state.
- Put the most important word first in each label.
- Follow left-to-right, top-to-bottom order, unless the design needs a different path.
- Set initial focus on every screen.
- Trap focus in dialogs and restore it when they close.
- Announce changes that happen without a focus move.
