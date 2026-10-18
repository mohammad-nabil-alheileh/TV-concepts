# Focusable vs. non-focusable

## 1. Focusable vs. non-focusable

A **focusable** element can receive focus and can be pressed with Select. A **non-focusable** element is skipped by the focus engine, so the remote moves straight past it.

| Component | Focusable on TV? |
|---|---|
| Touchable components | **Yes**, by default |
| `View` | No |
| `Text` | No |
| `Image` | No |

- Control focusability with the `focusable` prop.
- `disabled` also removes an element from focus.

## 2. `onFocus` / `onBlur`

These fire when an element gains or loses focus. TV users have no cursor, so **you must show focus visually**, or they can't tell where they are.

```jsx
function Card({ title }) {
  const [focused, setFocused] = useState(false);

  return (
    <Pressable
      onFocus={() => setFocused(true)}
      onBlur={() => setFocused(false)}
      onPress={() => open(title)}
      style={[
        styles.card,
        focused && styles.cardFocused, // e.g. scale 1.1 + border
      ]}
    >
      <Text>{title}</Text>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  card: { width: 300, height: 170, borderWidth: 3, borderColor: 'transparent' },
  cardFocused: { borderColor: 'white', transform: [{ scale: 1.08 }] },
});
```

## 3. `hasTVPreferredFocus`

When a screen appears, the system needs to know which element should get focus first. Without a hint, the engine picks one on its own, which is rarely what you want.

```jsx
function Home() {
  return (
    <View>
      <Pressable>
        <Text>Search</Text>
      </Pressable>

      {/* Focus starts here when the screen mounts */}
      <Pressable hasTVPreferredFocus onPress={resume}>
        <Text>Resume watching</Text>
      </Pressable>
    </View>
  );
}
```
