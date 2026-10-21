# Debug Exercise: Clipping and Layout Failures

Focus goes to the right element, but it looks wrong:

- A card is cut off at the edge.
- The focused card's zoom effect gets chopped.
- Text is truncated.
- Things sit in the wrong place on one TV but not another.

## Why TV Layouts Fail More Than Mobile

| Factor | What it means |
|---|---|
| Overscan and safe area | Some TVs crop the outer edge of the picture, so content right at the edge can be invisible |
| Focus effects need extra room | A focused card usually grows or gets a border. That extra space must exist somewhere |
| Many screen sizes | The same app runs on 720p, 1080p, and 4K TVs, and a layout tuned on one can break on another |
| Viewing distance | You sit about 3 meters away, so text and targets must be bigger than on mobile |

## Common Causes

| Cause | What it looks like |
|---|---|
| Parent has `overflow: 'hidden'`, or a list clips its content | The focused card's scale-up effect is cut off |
| No padding inside a horizontal list | The first or last card's focus effect is clipped at the screen edge |
| Content placed at the very edge | Cut off on TVs with overscan |
| Fixed pixel sizes everywhere | Fits on one screen size, overflows or leaves gaps on another |
| Long text with no limit | Titles push other elements out of place |

## Fixed Sizes vs Flexible Layouts

| Approach | Pros | Cons |
|---|---|---|
| Fixed sizes | Simple, predictable on one screen | Breaks when screen size or density changes |
| Flexible layout | Adapts across 720p, 1080p, and 4K | Harder to get an exact design, and can behave unexpectedly in nested lists |
| Scale values from a base | Matches the design while adapting to screen size | Needs a helper, and a wrong base causes blurry or huge UI |
