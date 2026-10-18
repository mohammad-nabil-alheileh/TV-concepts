# How focus works on web

The web TV has **no spatial navigation**. It only knows **Tab focus**, which follows DOM order, and the arrow keys just scroll the page. If you press Right, nothing meaningful happens. You have to supply that logic yourself.

## Part A: the spatial navigation library (Norigin)

Norigin Spatial Navigation listens for arrow keydown events, measures each focusable element, picks the nearest one in that direction, and tells your component it is now focused.

### Key pieces

| Piece | Purpose |
|---|---|
| `init()` | Starts listening for key events (call once) |
| `useFocusable()` | Hook that gives a component a `ref`, `focused`, and `focusSelf` |
| `FocusContext.Provider` | Groups children into a focus container (like a row) |
| `setFocus('KEY')` | Moves focus programmatically, e.g. to the first card on load |
| `onEnterPress`, `onArrowPress` | Handle OK and arrow behavior |
| `saveLastFocusedChild` | Returning to a row restores the last card |

## Part B: RN focus APIs mapped onto react-native-web

`react-native-web` turns `View` and `Pressable` into DOM elements, so some focus features carry over and some don't.

| Feature | On web |
|---|---|
| `focusable` | **Works.** Becomes `tabIndex`. |
| `onFocus` / `onBlur` | **Works.** Uses DOM focus events. |
| `hasTVPreferredFocus` | **Doesn't exist on web.** |
| `nextFocus*` | **Doesn't exist on web.** |
| `TVFocusGuideView` | **Doesn't exist on web.** |

So the pattern is a **platform-split wrapper**. Your screens use one `<Focusable>` component, and each platform implements it its own way:
