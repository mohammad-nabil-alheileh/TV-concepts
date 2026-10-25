# Scene Layering

A TV screen is usually a **stack of layers**, drawn back to front. Large artwork gives the screen its cinematic feel, but text on top of it has to stay readable. Layering is how you get both.

## The Four Layers (Back to Front)

| # | Layer | What it is | Example |
|---|---|---|---|
| 1 | Background artwork | Full-screen backdrop image or video | Movie backdrop, show key art |
| 2 | Scrim | A semi-transparent gradient between the art and the content | Dark gradient on the left and bottom |
| 3 | Content | Hero text, rails, grids, buttons | Title, description, Play button, rails |
| 4 | Overlays | Things that appear above everything | Side menu, modal, toast, loading spinner, player controls |

## 1. Background Artwork

The image fills the whole screen behind everything. It changes based on the focused item. For example, when the user moves to a different card, the backdrop switches to that item's art.

## 2. Scrim

A scrim is a gradient from transparent to dark.

- Without it, white text on a bright image is unreadable.
- It is usually darker where the text sits.

## 3. Content

The normal layout on top of the scrim: title, metadata, buttons, and rails.

## 4. Overlays

Anything that must sit above the rest, such as a side navigation drawer, a dialog, or a loading indicator.

- They render **last** in the tree, so they draw on top.
