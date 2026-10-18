# Old browser engines on LG and Samsung TVs

An LG or Samsung TV runs your app inside the web engine that shipped with that TV's firmware. There is no browser update, so **the oldest TV you support decides what your JavaScript bundle is allowed to contain**.

If you ship syntax the engine can't parse, the script doesn't run at all. The user just sees a **blank screen with no useful error**.

## Why it's worse than it looks

| Problem | What it means | What happens to your app |
|---|---|---|
| **Engines never update** | A community guide notes that once LG releases a webOS major version, it never updates that version's Chromium. | The engine you test against today is the engine users have for years. |
| **Old engines can't parse modern syntax** | A modern bundle may use syntax the engine doesn't understand. | The script never runs, so the user sees a blank screen. |

## Things to do

1. **Pick your oldest target, then compile down to it.** Transpile your bundle so it only uses syntax that target can parse.
2. **Debug with a matching Chrome.** Use a Chrome version close to the TV's engine, not your current one.
   - Remote debugging old TVs from a new Chrome can fail.
