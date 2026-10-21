# Feature Detection

Check for the capability you need, not the brand, model, or OS version that you assume has it.

## Why It Matters on TV

- **The TV market has a huge range.** There are dozens of model years per brand, each with a different engine version.
- **The LG and Samsung targets run your app inside the TV's built-in web engine.** You cannot update that engine, and older models stay in homes for 8 to 10 years.
- **Device lists go stale.** A check like `model === 'X'` breaks when a new model ships, and it is wrong for models you never tested.

## Polyfills for Old Engines

A polyfill adds a missing feature, so you can write modern code and still run on old engines.

## When a Device Check Is Still Acceptable

| Case | How to handle it |
|---|---|
| A known bug in one specific engine that you cannot detect by feature | Keep the check in one place, comment why, and note when you can remove it. |
| Analytics and logging, where you want the model name for reports | Use the device check only for reporting, not for changing behaviour. |
