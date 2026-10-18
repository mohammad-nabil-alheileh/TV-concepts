# Rails and grids

This topic covers designing for the most common case: **the user moves away from a list and then comes back to it.**

## Terms

| Term | Meaning |
|---|---|
| **Rail** | A horizontal list of cards. |
| **Grid** | A multi-column list. |

## The problem

Two situations break the default behavior:

| Situation | Example | What goes wrong |
|---|---|---|
| **Moving between rails** | The user is on card 7 of a row, presses Down, then Up. | The engine picks the geometrically closest element, which may be card 3 instead of card 7. |
| **Returning to a screen** | The user opens a details screen from card 12 and presses Back. | If the home screen remounted, focus resets to the top-left and card 12 is forgotten. |

**So you need to remember what was focused and restore it by a stable id.**

## Approaches

| Approach | Scope | How it works |
|---|---|---|
| **1. `TVFocusGuideView` with `autoFocus`** | Within a screen | Wrap each rail in a guide. When focus enters the guide, it picks a child itself, often the last focused one, instead of the closest by geometry. |
| **2. Save the focused id, restore with `hasTVPreferredFocus`** | Across screens | Save the id when an item gains focus. When the screen renders again, give preferred focus to the item that matches the saved id. |
