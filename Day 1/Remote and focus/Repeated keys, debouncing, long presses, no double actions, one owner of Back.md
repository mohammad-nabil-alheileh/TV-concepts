1. Repeated keys

    When a user holds a direction key, many platforms send a stream of repeated key-down events. That’s useful for fast scrolling, but it causes problems when a repeated key triggers something that should happen once.

        Fix: decide per action whether it should repeat.

            Action	Should repeat?
            Scrolling, seeking	Yes 
            Select, Play/Pause, Back	No, run once per press


2. Debouncing and throttling

    Throttle: run at most once per interval. It’s good for held-key scrolling or seeking.
    Debounce: wait until the input stops, then run once. It’s good for work triggered by focus changes.
    Lock: ignore further presses until the current action finishes. It’s good for navigation and purchases.


3. Long presses

    A long press is a held Select. Use it for secondary actions while a normal press does the main one.


4. No double actions:


    Repeated key-down events (held key). Run once per press.
    Several global handlers. Two mounted screens both react. Register handlers only while the screen is active.
    Press and long press both firing.
    Slow async actions. The user presses again before the first finishes. Use a lock or disable the button.
    Stale listeners. A missing cleanup leaves old handlers running.


5. One owner of Back

    The problem: the screen, a menu, a modal, a video player, and the navigation library may all want Back. Handlers run most-recent first, so the winner depends on mount order, which is fragile. Then a hidden component swallows Back, or Back exits the app from inside a modal.

        The fix: a single owner registers one BackHandler listener for the whole app. Everything else asks that owner through a stack of “back layers”. The most recently opened layer is closed first.