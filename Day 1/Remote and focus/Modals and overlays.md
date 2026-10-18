# Modals and overlays

This topic covers a special case: a dialog, menu, or overlay opens on top of the screen, and **the user must stay inside it until it closes.**

## The problem

On a TV, the focus engine doesn't know the background is "covered." If you do nothing:

| Problem | What happens |
|---|---|
| **Focus doesn't move in** | Focus stays on the button that opened the modal, behind the overlay. |
| **Focus escapes** | The user presses Down and lands on a card hidden under the dim layer. |
| **Focus is lost on close** | The opener unmounted or the screen re-rendered, so focus resets to the top-left. |

## Approach 1: the native `Modal` component

```jsx
import { Modal, Pressable, Text, View } from 'react-native';

<Modal visible={open} transparent onRequestClose={() => setOpen(false)}>
  <View style={styles.backdrop}>
    <Pressable hasTVPreferredFocus onPress={confirm}>
      <Text>Confirm</Text>
    </Pressable>
    <Pressable onPress={() => setOpen(false)}>
      <Text>Cancel</Text>
    </Pressable>
  </View>
</Modal>
```

## Approach 2: an in-tree overlay with a focus trap

Render the overlay inside your screen, and wrap it in a `TVFocusGuideView` that traps all four directions. Put `hasTVPreferredFocus` on the primary action so focus moves in.

```tsx
import { useEffect, useRef, useState } from 'react';
import { BackHandler, Pressable, StyleSheet, Text, TVFocusGuideView, View } from 'react-native';

function Screen() {
  const [open, setOpen] = useState(false);
  const openerRef = useRef<any>(null);
  const wasOpen = useRef(false);

  // Restore focus to the opener after the modal closes
  useEffect(() => {
    if (wasOpen.current && !open) {
      openerRef.current?.requestTVFocus?.(); // available in recent react-native-tvos versions
    }
    wasOpen.current = open;
  }, [open]);

  // Back closes the modal first (only registered while it is open)
  useEffect(() => {
    if (!open) return;
    const sub = BackHandler.addEventListener('hardwareBackPress', () => {
      setOpen(false);
      return true; // consumed
    });
    return () => sub.remove();
  }, [open]);

  return (
    <View style={{ flex: 1 }}>
      <Pressable ref={openerRef} onPress={() => setOpen(true)}>
        <Text>Delete item</Text>
      </Pressable>

      {open && (
        <View style={StyleSheet.absoluteFill}>
          <TVFocusGuideView
            autoFocus
            trapFocusUp
            trapFocusDown
            trapFocusLeft
            trapFocusRight
          >
            <Pressable hasTVPreferredFocus onPress={confirm}>
              <Text>Confirm</Text>
            </Pressable>
            <Pressable onPress={() => setOpen(false)}>
              <Text>Cancel</Text>
            </Pressable>
          </TVFocusGuideView>
        </View>
      )}
    </View>
  );
}
```

## Comparing the two approaches

| | **Approach 1: `Modal`** | **Approach 2: in-tree overlay** |
|---|---|---|
| **Where it renders** | Separate layer above the screen | Inside your screen's tree |
| **Focus handling** | `hasTVPreferredFocus` on the primary action | `TVFocusGuideView` traps all four directions, plus `hasTVPreferredFocus` |
| **Back button** | `onRequestClose` | A `BackHandler` listener that is registered only while the overlay is open |
| **Focus restore on close** | Not shown in the example | Done manually with `requestTVFocus()` on the opener |
