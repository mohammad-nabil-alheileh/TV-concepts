# Why mobile patterns fail on TV

A TV remote has no touch surface. Any pattern that depends on touch **can't be performed at all**. Other patterns technically work but are **painful at ten feet**.

## Patterns that don't translate

| Mobile pattern | Why it fails on TV | TV replacement |
|---|---|---|
| **Swipe-to-open drawer** | No swipe gesture exists on a D-pad. Hidden menus are also undiscoverable. | A visible side menu that expands when focus moves left |
| **Pull-to-refresh** | Needs a touch drag. | A "Refresh" button, or automatic refresh |
| **Small tap targets** | Hard to read from across the room, and focus highlights on tiny items are easy to lose. | Large items with a clear focus state |
| **Gestures** (pinch, long-press, swipe-to-delete) | No way to perform them, and users can't discover them. | Explicit buttons or a context menu |

## Example: small targets vs. TV-sized targets

```jsx
// Mobile: 32px icon button, fine for a thumb
<Pressable style={{ width: 32, height: 32 }} />

// TV: bigger, with a visible focus state
<Pressable
  style={({ focused }) => ({
    width: 96,
    height: 96,
    borderWidth: focused ? 4 : 0,
    borderColor: 'white',
    transform: [{ scale: focused ? 1.1 : 1 }],
  })}
/>
```

**Takeaway:** On TV, make targets larger and make focus impossible to miss. The focus state is how the user knows where they are.
