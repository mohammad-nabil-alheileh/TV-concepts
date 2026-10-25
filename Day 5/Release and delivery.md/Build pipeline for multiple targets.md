# Build Pipeline for Multiple Targets

A build pipeline is an automated, repeatable process that takes your source code and produces signed, installable packages for every TV platform you support.

## Build Principles

| # | Principle | What it means |
|---|---|---|
| 1 | One codebase, per-target configuration | Each target needs its own settings, such as app ID, API URL, and which features are on. A common way to handle this is to pass the target as an environment variable. |
| 2 | Use the right runner for each target | Apple TV builds need macOS runners because Xcode only runs there. Android, Tizen, and webOS can build on Linux. |
| 3 | Automate signing safely | Keystores and certificates are stored as CI secrets, decoded at build time, and never committed to git. |
| 4 | Version everything together | One source of truth for the version number, and a build number that goes up on every run. Stores reject uploads that reuse an old build number. |
| 5 | Cache dependencies | Caching `node_modules`, Gradle, and CocoaPods can cut build time a lot. |

## Runner Requirements per Target

| Target | Runner | Extra requirements |
|---|---|---|
| Apple TV (tvOS) | macOS | Xcode |
| Android TV / Fire TV | Linux | None |
| Samsung (Tizen) | Linux | Tizen CLI installed in the CI image |
| LG (webOS) | Linux | webOS CLI installed in the CI image |
