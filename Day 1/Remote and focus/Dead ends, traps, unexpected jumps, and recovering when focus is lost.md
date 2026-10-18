# Dead ends, traps, unexpected jumps, and recovering when focus is lost

This topic covers what goes wrong when steering is missing or misconfigured, and how to fix it. These are the focus bugs users notice first.

## Overview

| Problem | What the user sees |
|---|---|
| **Dead end** | A direction press does nothing. |
| **Trap** | Focus enters a region and can't get out. |
| **Unexpected jump** | Focus lands somewhere surprising, like a distant element. |
| **Lost focus** | Remote keys seem dead, or focus resets to the top of the screen. |

## 1. Dead ends

**What it is:** The user presses a direction and nothing happens, because the engine finds no focusable element in that direction.

**Typical causes:**

- A button sits visually "below" but is offset sideways, so no element lies in the pressed direction.
- A target was made `focusable={false}` or `disabled`.
- Content that loads late isn't mounted yet.
- A bad `nextFocus*` target points to nothing.

> Some dead ends are intentional (the bottom of a list). The bug is when the user expects somewhere to go.

## 2. Traps

**What it is:** Focus enters a region and the user can't get out. Every direction leads back inside.

**Typical causes:**

- A `trapFocus*` guide is left active after it should have been removed.
- An overlay stays mounted and focusable while hidden.
- A modal doesn't release focus on close.

## 3. Unexpected jumps

**What it is:** Focus lands somewhere surprising, like leaping to a distant element.

**Typical causes:**

- The engine picks the "closest" element, and the geometry isn't what you assumed.
- Several elements have `hasTVPreferredFocus`.
- Items re-mount when state changes.
- A `TVFocusGuideView` with `autoFocus` sends focus to a child you didn't expect.
- A late-loading element grabs preferred focus after the user has started navigating.

## 4. Recovering when focus is lost

**What it is:** The focused element disappears (unmounted, hidden, or disabled), and focus is left on nothing. Remote keys may seem dead, or focus resets to the top of the screen.

**Typical causes:**

- The user presses Select on an item that then removes itself.
- A loading spinner replaces the content that held focus.
- A screen transition unmounts the focused element.
