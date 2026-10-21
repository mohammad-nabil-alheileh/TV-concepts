# Startup on Slow TVs

Startup time is how long the user stares at a splash screen before they can press anything. On a slow TV chip, everything your app does before the first screen is **multiplied by 5 to 10** compared with your dev machine.

The goal is to do the minimum before the first usable screen, and push everything else later.

## Where Startup Time Goes

| Stage | Why it costs time |
|---|---|
| Loading and parsing the JS bundle | A bigger bundle means more time |
| Running module-level code | Every import runs its top-level code, even if the screen is never opened |
| Initial data fetching | Waiting for the network before rendering anything |
| First render | Mounting too many components at once |

## Part 1: Bundle Size

Import only what you use. Importing a whole library pulls all of it into the bundle.

```js
// Bad: pulls the whole library into the bundle
import _ from 'lodash';
import moment from 'moment';

// Better: import only what you use, or use smaller alternatives
import debounce from 'lodash/debounce';
import { format } from 'date-fns';
```

| Action | Notes |
|---|---|
| Use Hermes | It is the default in recent React Native. Verify it is enabled for your TV target. |
| Remove unused libraries and assets | Delete anything the app no longer uses |
| Compress bundled images and fonts | Smaller assets mean a smaller app package |

## Part 2: Lazy Loading

Lazy loading delays loading code until it is needed. The approach depends on the platform.

### React Native (Android, iOS)

Enable inline requires in `metro.config.js`, so modules run only when first required:

```js
// metro.config.js
module.exports = {
  transformer: {
    getTransformOptions: async () => ({
      transform: { experimentalImportSupport: false, inlineRequires: true },
    }),
  },
};
```

### Web-based Platforms (LG, Samsung)

Use `React.lazy` with `Suspense` to load a screen only when it is rendered:

```jsx
const SettingsScreen = React.lazy(() => import('./screens/SettingsScreen'));

<Suspense fallback={<Spinner />}>
  <SettingsScreen />
</Suspense>
```

## Other Ways to Shorten the Startup Path

| Technique | What it does | Effect on startup |
|---|---|---|
| Render first, fetch after | Show a skeleton immediately instead of waiting for the network | The first screen appears without waiting for data |
| Cache the last home screen response | Save the response on disk and show it right away | Users see content immediately, even offline |
| Refresh in the background | Update the cached content after it is shown | Content stays current without delaying the first screen |
| Mount the first rails only | Render only the first rail or two at startup, and mount the rest after | Reduces the work of the first render |
