# Remote Debugging Tools

The TV has no keyboard, no terminal, and no visible logs. Remote debugging means your computer connects to the TV over the network and shows you what the app is doing. Each platform has its own tool:

| Platform | Tool |
|---|---|
| React Native | React Native DevTools / Metro |
| Android TV / Fire TV | logcat |
| Apple TV | Xcode |
| Samsung / LG (web builds) | Chrome DevTools via Tizen Studio / webOS inspector |

## Tools in Detail

| Tool | What it is | Good for |
|---|---|---|
| React Native DevTools | The TV connects to Metro on your computer. The dev menu is opened with a remote shortcut. | JS errors, state bugs, API calls |
| logcat | Android's system log. Captures native logs, JS `console.log`, and crash stack traces. | Native crashes, out-of-memory kills, "the app just closed" bugs |
| Xcode | Run the app from Xcode with the Apple TV selected as the target. | Memory leaks, native crashes, focus-engine problems |
| Chrome DevTools | Because these run as web apps, you use the browser inspector. | Web-app debugging on Samsung and LG |

