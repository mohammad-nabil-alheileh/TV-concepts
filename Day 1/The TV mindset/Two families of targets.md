# Two families of targets

"React Native on TV" covers **two different technical families**, and they behave differently.

## Comparison

| | **Native family** | **Web family** |
|---|---|---|
| **Targets** | Android TV, Apple TV (tvOS) | LG (webOS), Samsung (Tizen) |
| **What runs** | Real native views, with your JS in a JS engine | A web app inside the TV's built-in browser |
| **Bundler** | Metro | webpack |
| **Output** | `.apk` / tvOS app via Android Studio / Xcode | Packaged web app |
| **Focus handling** | Provided by the native focus engine | Mostly yours to build in the DOM |

## Web family

### How it works

- Tell webpack to swap `react-native` for `react-native-web`, so the same components render as `<div>`.
- There is no native focus engine here, so **you handle remote keys yourself**.

### Handling remote keys

```js
window.addEventListener('keydown', (e) => {
  switch (e.keyCode) {
    case 37: moveFocus('left');  break;
    case 38: moveFocus('up');    break;
    case 39: moveFocus('right'); break;
    case 40: moveFocus('down');  break;
    case 13: pressOk();          break;
    case 461:   goBack(); break;   // LG webOS Back
    case 10009: goBack(); break;   // Samsung Tizen Back
  }
});
```

| Key code | Remote key | Action |
|---|---|---|
| 37 | Left | `moveFocus('left')` |
| 38 | Up | `moveFocus('up')` |
| 39 | Right | `moveFocus('right')` |
| 40 | Down | `moveFocus('down')` |
| 13 | OK | `pressOk()` |
| 461 | Back (LG webOS) | `goBack()` |
| 10009 | Back (Samsung Tizen) | `goBack()` |

Back uses a different key code on each platform, so you need both cases.

## Sharing code between both families

Share the logic, and keep the platform-specific parts in separate files.
