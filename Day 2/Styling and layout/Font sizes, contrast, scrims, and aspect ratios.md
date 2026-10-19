# Font Sizes, Contrast, Scrims, and Aspect Ratios

A TV is read from about 3 meters (10 feet) away, on a screen that is dimmer to read than a phone, and the user navigates with a remote instead of touch. Text that looks fine on a laptop becomes hard to read on a TV.

Four rules fix most of these problems:

1. Make text bigger than you would on mobile or web.
2. Keep contrast high, but avoid pure white on pure black.
3. Put a scrim (a dark gradient or overlay) between artwork and text.
4. Plan for aspect ratios, because artwork gets cropped.

## 1. Font sizes

Use these sizes as a starting point at the 1920x1080 design size:

| Use                    | Design size (1920x1080) |
| ---------------------- | ----------------------- |
| Hero title             | 56 to 72 px             |
| Section title          | 36 to 44 px             |
| Card title / body      | 28 to 32 px             |
| Caption (the floor)    | 24 px                   |

**Caption is the smallest allowed size.** Do not go below 24 px in the design space, even for secondary text.

Scale these values with the same scale factor as the rest of the layout. See the scaling topic.

## 2. Contrast

| Do                                                    | Don't                                                       | Why                                                  |
| ----------------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------------------- |
| Use off-white text (for example, a light gray) on dark backgrounds | Use pure white text on pure black        | Pure white on pure black glows and causes eye strain at distance |
| Use regular or bold weights for body and small text   | Use thin font weights for small text                        | Thin strokes vanish at distance                      |
| Add an icon or a word next to a color                 | Use color alone to show meaning                             | Users with color blindness may not see the difference |

## 3. Scrims over artwork

Text placed directly on a poster or hero image is unreadable on bright areas of the image. A **scrim** solves this. It is a gradient that goes from transparent to dark, placed between the image and the text.

Layer the elements in this order, from back to front:

| Layer | Element         | Purpose                              |
| ----- | --------------- | ------------------------------------ |
| 1     | Artwork (image) | Background visual                    |
| 2     | Scrim (gradient) | Darkens the area behind the text    |
| 3     | Text            | Readable content on top of the scrim |

Place the scrim only where the text sits. Keep the rest of the artwork bright so it still looks good.