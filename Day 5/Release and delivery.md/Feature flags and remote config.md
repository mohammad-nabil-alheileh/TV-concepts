# Feature Flags and Remote Config

| Term | Meaning |
|---|---|
| **Feature flag** | A switch stored outside your app's code. It turns a feature on or off, or changes who sees it, without shipping a new build. |
| **Remote config** | key-value settings the app fetches at launch or at runtime, such as API URLs, timeouts, text, layout options, and flag values. |

## Common Uses on TV

| Use | Example |
|---|---|
| Platform-specific switches | Turn off a heavy animation only on low-end Samsung or LG models. |
| Gradual feature release | Enable a new player for 10% of users first. |
| Workarounds | Disable a feature that crashes on one TV brand while you prepare a fix. |
| A/B tests | Compare two home screen layouts. |
