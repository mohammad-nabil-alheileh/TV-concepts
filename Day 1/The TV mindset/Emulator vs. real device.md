# Emulator vs. real device

Every TV platform gives you a way to run your app on your computer.

## Emulators by platform

| Platform | Emulator |
|---|---|
| **Android TV** | Android Studio emulator (AVD) |
| **Apple TV** | tvOS simulator in Xcode |
| **LG webOS** | webOS TV emulator/simulator |
| **Samsung Tizen** | TV emulator in Tizen Studio |

Emulators are great for **fast daily work**. But an emulator runs on your computer's CPU, RAM, and keyboard. It can't tell you how the app behaves on the weak hardware and real remote your users have.

## What an emulator cannot tell you

| Question | Why the emulator misleads you |
|---|---|
| **Is it fast enough?** | Your laptop is far stronger than a TV's CPU, so lag and stutter won't show up. |
| **Will it run out of memory?** | The emulator has far more RAM headroom, so "app killed" crashes don't happen. |
| **Does the real remote work?** | Keyboard arrows are not a remote. Real remotes have different key codes, a Back button with vendor-specific behavior, voice and color buttons, and key-repeat timing. |
| **Is the web engine behavior identical?** | The emulator is close, but real firmware can differ, and your oldest supported TV may behave differently than the emulator image. |
| **Does it look right?** | Real panels differ in color, brightness, and overscan (edges cropped on some TVs). Text that looks fine on a monitor may be hard to read from the couch. |
| **How does the real network behave?** | Slow Wi-Fi on a TV is common and rarely reproduced on a developer machine. |

**Takeaway:** Use emulators for daily development, and test on a real device before release. Include your oldest supported TV in that testing.
