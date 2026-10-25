# Staged Rollout and Kill Switch

| Term | Meaning |
|---|---|
| **Staged rollout** | Releasing a new version to a small percentage of users first, then increasing the percentage as it proves stable. |
| **Kill switch** | A remote control that instantly turns off a feature when something goes wrong, without waiting for a store update. |

Together they limit the damage of a bad release. If a bug only reaches 5% of users, and you can turn the broken part off in minutes, the problem stays small.

## Part 1: Staged Rollout

### How Each Store Supports It

| Platform | Staged rollout support |
|---|---|
| Google Play | Built in. You choose a percentage and can halt it at any time. |
| Apple tvOS | Phased release over 7 days is available for automatic updates. You can pause it, but it isn't a custom percentage. |
| Samsung Tizen | Check Seller Office for current options. Gradual percentage control may be limited. |
| LG webOS | Check Seller Lounge for current options. Same caution. |

### What to Watch

- Crash-free sessions
- App launch failures
- Playback errors
- Network error rates
- Store ratings and reviews
- Support complaints

## Part 2: Kill Switch

A **feature-level kill switch** is a remote flag that disables one feature.

```jsx
function PlayerScreen() {
  // Kill switch: flip to false on the server to stop using the new player
  return flag("newPlayerEnabled") ? <NewPlayer /> : <OldPlayer />;
}
```
