# Store Certification Requirements

Before a store lists your app, it reviews it against a set of rules. Each TV platform has its own checklist, and a signed package that works fine can still be rejected for failing it.

## What Every Store Checks (The Common Core)

| Check | What it means |
|---|---|
| Remote-only navigation | Every screen and action must work with the D-pad, OK, and Back buttons. |
| Visible focus | The user must always be able to see which element is focused. |
| Back button behavior | Back goes to the previous screen. On the home screen it exits the app or asks for confirmation, depending on the store. |
| Stability | No crashes, freezes, or blank screens, including when the network is slow or offline. |
| Performance | The app must launch in a reasonable time and not run out of memory on low-end TVs. |
| Legal and content | A privacy policy, correct content rating, and accurate descriptions. |
| Correct assets | The right icon, banner, screenshot, and splash sizes for each store. |

## Platform by Platform

### Google Play

- Follows the manifest rules: leanback launcher, banner, and touchscreen not required.
- Must meet Google's TV app quality guidelines, such as D-pad navigation, focus, landscape layout, and text that stays readable from a distance.
- Needs screenshots and a banner in the sizes Play requires, plus the **Data safety** form.

### Samsung Tizen

- The app is tested on real Samsung TVs by Samsung's reviewers.
- Typical checks:
  - Remote control keys work.
  - The Return key behaves correctly.
  - The app handles network loss.
  - Launch time and memory use are acceptable.
- You provide **test accounts** if the app has a login, so reviewers can get past it.

### LG webOS

- LG has its own QA checklist, covering Magic Remote pointer and D-pad behavior, the Back key, and launch and exit handling.
- The app must handle the webOS lifecycle, such as being sent to the background and resumed.

### Apple tvOS

- Follows Apple's Human Interface Guidelines for tvOS, including Siri Remote navigation and the focus engine.
- Requires **layered app icons** and a **Top Shelf** image.
- Apple's general rules apply too:
  - Privacy labels.
  - In-app purchase rules.
  - Account deletion, if you support account creation.
