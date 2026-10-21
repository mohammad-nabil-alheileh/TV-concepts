# Virtualised Rails and Focus

A virtualised list (FlatList, FlashList) only keeps the items near the viewport mounted. Items that scroll far away are unmounted to save memory.

The problem is that **focus lives on a mounted view**. If the focused item unmounts, focus is lost. And if the next item the user is heading toward isn't mounted yet, the D-pad has nothing to move to.

## Why It Matters on TV

A rail with 200 posters can't render everything on a low-RAM TV, so you need virtualisation.

## Three Things That Go Wrong

| Problem | What the user sees | Cause |
|---|---|---|
| Focus lost on unmount | The user holds right, the list scrolls, and focus jumps to the first item, or to nothing | The window drops the focused item while it is still focused |
| Dead end | The user presses right, but nothing happens | The next item isn't rendered yet, so the focus engine finds no target |
| Focus not restored | After returning from a details screen, focus lands on item 0 | The rail remounts and loses its previous position |
