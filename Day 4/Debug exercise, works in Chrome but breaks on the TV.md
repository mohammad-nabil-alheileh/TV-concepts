# Debug Exercise: Works in Chrome but Breaks on the TV

The app runs fine in desktop Chrome, but on the TV you get:

- A blank white or black screen.
- A missing feature.
- Broken styling.

## What Breaks

| Category | Examples | What happens |
|---|---|---|
| Newer JS syntax | `?.` (optional chaining), `??` (nullish), class fields | `SyntaxError`: the whole bundle fails to parse, giving a blank screen |
| Newer JS APIs | `Array.prototype.flat`, `Object.fromEntries`, `String.prototype.replaceAll`, `Promise.allSettled`, `structuredClone`, `.at()` | `TypeError: x is not a function` at runtime |
| Newer web APIs | `ResizeObserver`, `IntersectionObserver`, `AbortController` | Features silently fail or crash |
| Newer CSS | Flexbox `gap`, `aspect-ratio`, `inset`, `:focus-visible`, some grid features | Layout collapses or spacing disappears with no error |

## Ways to Prevent It

| Tool | Purpose |
|---|---|
| `browserslist` | Tells Babel and Autoprefixer which engines to support |
| Babel / SWC | Rewrites newer syntax |
| `core-js` | Polyfills missing JS APIs |
| Autoprefixer / PostCSS | Adds CSS prefixes |
| `eslint-plugin-compat` | Warns when you use an API your targets lack |
| Testing on real devices | The only proof of what the engine really does |

## Modern Code with Transpiling vs Writing for the Old Engine

| Approach | Pros | Cons |
|---|---|---|
| Write modern code, transpile and polyfill | Clean code, normal developer experience, one codebase | Larger bundle, slower startup on weak TVs, and polyfills can't fix everything |
| Write conservatively for the oldest engine | Smaller bundle, fewer surprises | Harder to write, and easy to slip back into modern features without noticing |
| Raise the minimum supported TV year | Less work, newer features available | You drop customers with older TVs |
