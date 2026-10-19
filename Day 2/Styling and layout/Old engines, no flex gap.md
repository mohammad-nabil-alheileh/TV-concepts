# Old Engines and Flexbox Gap

TV web apps run inside the TV's built-in browser. That browser is frozen at whatever version shipped with the TV's firmware, and many TVs never receive updates.

Newer CSS features, including `gap` on flexbox, may **silently do nothing** on these engines. The code runs without errors, but the spacing disappears.

## The problem

This code looks correct on a new TV and in a modern desktop browser:

```tsx
// Looks perfect on a new TV and in a modern desktop browser
<View style={{ flexDirection: 'row', gap: 24 }}>
  <Card />
  <Card />
  <Card />
</View>
```

On an old engine, the three cards are glued together with no space between them.

## Fallbacks

Use one of these three options instead of `gap`.

| Option | Approach | Best for |
| ------ | -------- | -------- |
| 1. Margin on items | Add `marginRight` to every item except the last | Any row of custom children |
| 2. Spacer elements | Insert a fixed-width `Gap` view between items | Small, fixed layouts |
| 3. List separators | Use `ItemSeparatorComponent` in a `FlatList` | Lists and carousels |

### Option 1: Margin on the items

```tsx
function Row({ children }: { children: React.ReactNode }) {
  const s = useScale();
  const items = React.Children.toArray(children);

  return (
    <View style={{ flexDirection: 'row' }}>
      {items.map((child, i) => (
        <View key={i} style={{ marginRight: i < items.length - 1 ? s(24) : 0 }}>
          {child}
        </View>
      ))}
    </View>
  );
}
```

### Option 2: Spacer elements

```tsx
const Gap = ({ size }: { size: number }) => <View style={{ width: size }} />;

<View style={{ flexDirection: 'row' }}>
  <Card />
  <Gap size={s(24)} />
  <Card />
</View>
```

### Option 3: List separators (for FlatList)

```tsx
<FlatList
  horizontal
  data={items}
  ItemSeparatorComponent={() => <View style={{ width: s(24) }} />}
  renderItem={({ item }) => <Card title={item.title} />}
/>
```

## Rules

- Do not rely on `gap` for any layout that must work on TVs.
- Use the scale helper (`s(24)`) for every spacing value, so the gap scales with the screen. The problem example uses a fixed `24` only to show the failure.
