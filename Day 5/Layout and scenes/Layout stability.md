# Layout Stability

On TV, the user steers with a D-pad, so focus has to land on something that **stays put**. If a card moves while the user is pressing a direction, they lose their place or press the wrong item.

## What Causes Layout Shifts

| Cause | Example |
|---|---|
| Images loading | A card is 0 tall, then jumps to full height when the image arrives |
| Data loading | A rail appears after a fetch and pushes everything below it down |
| Text length | A long title wraps to two lines and makes one card taller than its neighbors |
| Focus scaling done with layout | The focused card grows in width/height, so its neighbors get pushed away |
| Conditional content | A "New" badge or progress bar appears and changes a card's height |

## Three Tools to Fix It

### 1. Fixed-Size Containers

Give every card, rail, and section an explicit size before any content arrives. Content then fits inside the box. The box never reacts to its content.

### 2. Skeleton Placeholders

While data loads, render gray boxes with the same dimensions as the real content. When the data arrives, the real cards replace them with no movement.

### 3. No Shifting While Navigating

Anything that happens when focus moves must not change the layout. The main case is the focus effect.

Other things to keep stable while navigating:

| Element | How to keep it stable |
|---|---|
| Focus border | Always draw a transparent 3px border and only change its color |
| Scaled focused card | Leave vertical room in the rail so the card is not clipped |
| Badges and "Play" overlays | Do not insert or remove views next to the focused item; keep them rendered and toggle opacity |
| Hero or background art | Changing it when focus moves must not change the content's size |
