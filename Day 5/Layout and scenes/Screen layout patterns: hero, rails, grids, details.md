# Screen Layout Patterns: Hero, Rails, Grids, Details

On TV you design for a **10-foot UI**: big items, few on screen, navigated with a D-pad (remote). Almost every TV screen is built from four patterns.

## The Four Patterns

| Pattern | What it is | Navigation | Typical use |
|---|---|---|---|
| **Hero** | One large featured item at the top of the screen. | Usually the first focus target; moves down into the rails. | Promoting one show, movie, or event. |
| **Rail** | A horizontal row of cards with a title. Rails are stacked vertically. | Left/right moves within a rail; up/down moves between rails. | Categories such as "Continue Watching" or "Trending". |
| **Grid** | Items arranged in rows and columns. | Every item is reachable in 4 directions (up, down, left, right). | Browse, search results, "All episodes". |
| **Details** | A screen about one single item. | Focus moves between actions (play, add to list) and related content. | After the user picks something. |

## A Typical Home Screen

A home screen is usually a **hero on top** and a **vertical list of rails** below it.

- The **outer list** scrolls vertically.
- Each **rail** is a horizontal list inside that outer list.

```
+-----------------------------------------+
|                  HERO                   |
+-----------------------------------------+
| Title of rail 1                         |
| [card][card][card][card][card] ->       |
+-----------------------------------------+
| Title of rail 2                         |
| [card][card][card][card][card] ->       |
+-----------------------------------------+
| Title of rail 3                         |
| [card][card][card][card][card] ->       |
+-----------------------------------------+
```

## Navigation Rules

| Direction | In a rail | In a grid | Between sections |
|---|---|---|---|
| Left / Right | Move to the previous / next card | Move to the adjacent item | Usually not used |
| Up / Down | Move to the rail above / below | Move to the row above / below | Move between rails or from hero to rails |

## When to Use Which

| Screen | Pattern |
|---|---|
| Home or discovery | Hero + rails |
| Full catalog, search results, library | Grid |
| After the user picks something | Details |
