# Focus and Navigation Smoke Tests

Replay a fixed set of remote key sequences on a real device or emulator, and check that focus lands where it should.

## Two Kinds of Smoke Test

| Kind | How it works | Run by |
|---|---|---|
| 1. Key sequence tests | A scripted list of key presses, with the result checked after each step | Automated |
| 2. Manual focus walk | A person walks through every screen with the remote and checks that everything is reachable and every route back works | Person |

### 1. Key Sequence Tests

Send a scripted list of key presses and check the result after each step.

```bash
# Home -> move down twice -> right once -> select -> back
adb shell input keyevent 20   # DPAD_DOWN
adb shell input keyevent 20   # DPAD_DOWN
adb shell input keyevent 22   # DPAD_RIGHT
adb shell input keyevent 23   # DPAD_CENTER (select)
adb shell input keyevent 4    # BACK
```

### 2. Manual Focus Walk

A person walks through every screen with the remote and answers one question: **can I reach everything, and can I always get back?**

A manual focus walk checks that:

- Every interactive element can receive focus.
- Focus is always visible.
- Focus never gets trapped.
- Directions behave predictably: Down, then Up, returns you to the same element.
- Back always does something sensible, from every screen and popup.
- Focus is restored when you return to a screen or close a popup.

## What a Good Smoke Test List Looks Like

Keep it small enough to run before every release, in a few minutes:

| # | Sequence | Expected |
|---|---|---|
| 1 | Launch app | Focus lands on the first card |
| 2 | Down x3, then Up x3 | Back on the starting element |
| 3 | Move to the end of a row, press Right | Focus stays on the last card, or follows your design, and does not get lost |
| 4 | Select a card, then Back | Returns to the same card with focus restored |
| 5 | Open a popup, press Back | Popup closes, screen behind stays |
| 6 | Press Back on the home screen | Exits as designed |
| 7 | Hold Right to scroll a long row | Smooth scroll, focus is not lost |

## Where to Run Them

| Where | Pros | Cons |
|---|---|---|
| Emulator | Quick, easy to automate | Layout and speed differ from real TVs |
| Real device | Shows real geometry, overscan, and speed | Slower, harder to automate, and one device may not represent others |
| Several devices | Best coverage | Costs time and hardware |
