# TV Troubleshooting Workflow

TV bugs are hard to debug. You can't open DevTools and click around. You have a remote, a slow device, and often no debugger. A fixed routine stops you from guessing.

## The Five Steps

| Step | Goal | Question to answer |
|---|---|---|
| 1. Reproduce | Find a reliable way to trigger the bug | What exact key sequence, on which screen, on which device? |
| 2. Classify | Pick the bug category | Which kind of problem is this? |
| 3. Collect | Gather evidence for that category | What does the app actually report? |
| 4. Compare | Find what differs between working and broken | What changed between the good case and the bad case? |
| 5. One change | Fix it with a single, testable change | Did that one change fix it? |

### 1. Reproduce

Find the exact key sequence that triggers the bug, on which screen, on which device.

> **Example:** "On Home, press Down twice, then Right. Focus jumps to the header instead of the third row. It happens on the real Android TV but not on the emulator."

### 2. Classify

Decide which category the bug belongs to. Each category has different tools.

| Category | Symptom |
|---|---|
| Input | The key press never reaches the app |
| Focus | The key arrives, but the wrong element gets focus |
| Layout | The element is in the wrong place, clipped, or the wrong size |
| Performance | Everything is correct but slow, or memory climbs |
| Platform/engine | It works on one target and breaks on another |

### 3. Collect

Gather evidence for the category instead of reading code and guessing.

| Category | What to collect |
|---|---|
| Input | Log the raw key events |
| Focus | Log which element has focus |
| Layout | Log `onLayout` sizes, or turn on borders |
| Performance | Watch memory over time |
| Platform/engine | Capture logs from each target and compare them |

### 4. Compare

Find what differs between the working and broken cases:

| Compare | Working case | Broken case |
|---|---|---|
| Environment | Emulator | Real device |
| Code version | Last working commit | Today's build |
| Platform | Android TV | Apple TV |
| Resolution | 1080p | 4K |

### 5. One Change

Change one thing, then retest.

> If you change three things and the bug goes away, you don't know which change fixed it. You may also have added two new bugs.
