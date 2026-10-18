# Living room, ten-foot UI, and press cost

## The setup

On a TV, the user sits about **ten feet** away and navigates with a remote that has a **D-pad** (up, down, left, right), **OK**, and **Back**.

You can't point on a TV. The user moves a **focus highlight** from item to item, one press at a time.

## Two core ideas

| Idea | What it means | What to do |
|---|---|---|
| **Ten-foot UI** | Text, images, and focus highlights must be readable from across a room. | Use large fonts, high contrast, generous spacing, and a clear focus state. |
| **Press cost** | Every D-pad press costs the user time and effort. | Count how many presses a flow takes, then cut them. |

## Example: counting presses

**Goal:** Play the last episode of a show.

| Version | Path | Presses |
|---|---|---|
| **A** | Home → down to "Shows" row → right ×5 to find the show → OK → down to the season list → OK → down ×11 to the last episode → OK → OK to play | **≈ 22** |
| **B** | Home → "Continue watching" row is focused by default → OK | **1–2** |

**Takeaway:** Version B removes the search and navigation steps by putting the most likely action where focus already starts.

## Example: search

Typing with an on-screen keyboard costs several presses per letter, so good TV apps reduce typing:

- **Voice search** instead of typing
- **Recent searches** the user can select in one step
- **Suggestions** that appear as soon as the user starts typing
- **Fewer typing fields** overall
