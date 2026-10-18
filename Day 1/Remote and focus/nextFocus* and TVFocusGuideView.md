# nextFocus* and TVFocusGuideView

By default, the focus engine picks the **geometrically closest focusable element** in the direction pressed.

When that default is wrong, there are two tools to override it.

## 1. `nextFocus*`

These props are `nextFocusUp`, `nextFocusDown`, `nextFocusLeft`, `nextFocusRight`, and `nextFocusForward`.

Each one says: "When the user presses this direction from this element, move focus to that specific element." The target is given as a **native node handle**.

| Prop | Direction |
|---|---|
| `nextFocusUp` | Up |
| `nextFocusDown` | Down |
| `nextFocusLeft` | Left |
| `nextFocusRight` | Right |
| `nextFocusForward` | Forward |

```tsx
function Header() {
  const searchRef = useRef(null);
  const heroRef = useRef(null);
  const [searchTag, setSearchTag] = useState<number | null>(null);

  useEffect(() => {
    setSearchTag(findNodeHandle(searchRef.current));
  }, []);

  return (
    <View>
      <Pressable ref={searchRef}>
        <Text>Search</Text>
      </Pressable>

      {/* Pressing Up from the hero always goes to Search */}
      <Pressable ref={heroRef} nextFocusUp={searchTag ?? undefined}>
        <Text>Hero banner</Text>
      </Pressable>
    </View>
  );
}
```

## 2. `TVFocusGuideView`

An **invisible container** that redirects focus for you. You wrap a region, and it tells the focus engine where focus should go when it arrives.

It takes refs as `destinations`, so the engine can jump over empty space or land on a specific element.

```jsx
import { TVFocusGuideView } from 'react-native';

function Screen() {
  const playRef = useRef(null);

  return (
    <View>
      {/* A guide over an empty area: moving into it redirects to Play */}
      <TVFocusGuideView destinations={playRef.current ? [playRef.current] : []}>
        <View style={{ height: 80 }} />
      </TVFocusGuideView>

      <Pressable ref={playRef}>
        <Text>Play</Text>
      </Pressable>
    </View>
  );
}
```

| Tool | Purpose | Target |
|---|---|---|
| `nextFocus*` | Send focus from one element to a specific element in one direction | Native node handle |
| `TVFocusGuideView` | Redirect focus arriving in a region, including empty space | Refs passed as `destinations` |
