# Native Modules

A native module is code written in the platform's own language (Kotlin/Java on Android, Swift/Objective-C on iOS) that your JavaScript can call. React Native runs your JS in an engine, and JS cannot touch Bluetooth, the biometric prompt, a background service, or a vendor SDK directly. A native module is the bridge to those APIs.

## When You Need One

Work through these questions in order. Only write a native module if the answer to all of them is no.

| Question | If yes |
|---|---|
| Does React Native already expose it? | Use the built-in API. |
| Does a maintained community library exist? Check `react-native-*` and the React Native Directory. | Use the library. |
| Can a web API or plain JS do it? | Use that instead. |

## The Rules You Must Respect

| Rule | What it means |
|---|---|
| **Types are limited** | Strings, numbers, booleans, arrays, objects, and null cross the boundary. Anything else needs a plan. |
| **Threading matters** | UI work must run on the main thread. Slow work must stay off it. Mixing these up gives you frozen screens or crashes. |
| **Prefer async over sync** | A synchronous call blocks the JS thread until the native side returns. |
| **Permissions are separate** | Declare them in the manifest (Android) or `Info.plist` (iOS), and request them at runtime. |
| **Native changes need a new build** | Fast Refresh and OTA updates only cover JS, so you must rebuild the app. |
