# Rail Sizing and Peek

A rail is only useful if the user can tell:

1. How big the cards are.
2. How many fit on screen.
3. That there is more to the right.

The **peek** is the visual hint that tells the user the row scrolls.

## The Three Decisions

### 1. Card Size

Pick an **aspect ratio** first, then derive the card size from the screen.

| Card type | Ratio | Typical use |
|---|---|---|
| Landscape | 16:9 | Episodes, continue watching |
| Poster | 2:3 | Movies, series |
| Square | 1:1 | Music, apps, channels |

### 2. Visible Items

How many full cards fit on screen.

| Card type | Usually fits | Trade-off |
|---|---|---|
| Landscape | 4 to 6 | Fewer = bigger and easier to read from 10 feet |
| Poster | 6 to 7 | More = less scrolling, but smaller focus targets |

### 3. Peek

Show part of the next card instead of ending exactly on a card boundary.

| Style | Look | Notes |
|---|---|---|
| Hard edge (no peek) | Last card ends exactly at the edge | Looks tidy, but hides that more content exists |
| Small peek (~25%) | A sliver of the next card | Subtle, but may look like a layout bug |
| Half peek (~50%) | Half of the next card | The most common; clearly says "scroll" |
