# Component Tests for Focus and Key-Handling Logic

Write small automated tests (Jest and React Native Testing Library) that check your logic around focus and keys. They run on your computer in seconds, without a TV, an emulator, or a remote.

## What Component Tests Can and Can't Check

| Can check (your logic) | Can't check (the platform) |
|---|---|
| "When this key arrives, selection moves to the next index" | Where the real focus engine sends focus |
| "When a card gets focus, the highlight shows" | Clipping, overscan, and layout on a real screen |
| "Back closes the menu and is consumed" | Speed and memory on weak hardware |
| "The listener is removed on unmount" | Old-engine differences |
| "Pressing Select on a card calls `onPress`" | Whether the physical remote sends the key |

## Steps to do

Step 1: Separate the Logic from the Platform


Step 2: Test Focus Behaviour in a Component


Step 3: Test Back Handling


## Which Bugs Can These Tests Catch?

| Topic | Testable? |
|---|---|
| Input not detected | Partly. You can test that handlers react to events, but not that the remote delivers them |
| Focus jumps | Only your own logic, not the real geometry |
| Wrong Back | Yes, very well |
| Clipping and layout | No |
| Slow screen, memory | Partly. You can test that listeners and timers are cleaned up |
| Old engine | No |
