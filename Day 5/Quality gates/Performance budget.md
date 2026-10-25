Performance budget: numeric limits your app must stay within.

Release gate: the budget is enforced automatically in CI. If a build exceeds it, the release is blocked, the same as a failing unit test.

Soak test: running the app for a long time to find problems that only appear over time, like memory leaks, crashes, slowdowns, and battery drain.


Typical budget metrics in React Native
    Metric	Example budget	Notes
    Cold start 	≤ 2.5 s low tier, ≤ 1.5 s high tier	Hermes and lazy-loading screens help most
    JS bundle size	≤ 4 MB	Watch big libraries
    App install size	≤ 40 MB	Store limits and user download friction
    Frame rate / jank	≥ 55 FPS on key flows, < 2% slow frames	Measure on both the UI and JS threads
    Memory	≤ 300 MB peak on low tier	Low-end devices get killed by the OS first
    Screen render time	≤ 300 ms to show the list screen	Reassure can track render regressions



How to implement a gate
    Measure a baseline on your lowest-tier matrix device.
    Set the budget slightly above the baseline, not at an ideal number you can’t meet yet.
    Fail the build when a metric crosses the budget.



What soak tests commonly find in React Native:

    Event listeners and subscriptions not cleaned up in useEffect
    Timers and intervals that keep running after a screen unmounts
    Large images or lists holding memory
    Memory growth from storing too much in global state
    Crashes after hours caused by the OS killing the app for memory