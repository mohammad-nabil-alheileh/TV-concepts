# Debug Exercise: Remote Input Not Detected

## Symptom

You press buttons on the remote and nothing happens:

- No focus movement
- No `onPress`
- No logs

## First Question

**Did the key reach the app at all?**

This one question splits the bug in two:

| Answer | Where the problem is | Look at |
|---|---|---|
| The key never arrives | Below your code | Device, remote, build setup, or OS |
| The key arrives but nothing happens | In your code | Handler, focus, or event swallowing |

## Common Causes

| Cause | What it looks like |
|---|---|
| Not using the TV-enabled build | No TV events at all |
| Handler registered in a component that isn't mounted, or cleaned up too early | Works on one screen, silent on another |
| Element isn't focusable | Focus never lands on it, so `onPress` never fires |
| Something else is capturing keys | Keys work until a certain screen or popup |
| Remote differences | Works on the emulator keyboard but not on the real remote. Some remotes send keys the app doesn't expect, or the remote is in pointer mode instead of D-pad mode |
