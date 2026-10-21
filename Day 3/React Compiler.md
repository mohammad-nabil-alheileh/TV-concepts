# React Compiler

The React Compiler is a build-time tool that adds memoisation to your components for you.

Without it, you wrap values in `useMemo`, functions in `useCallback`, and components in `React.memo` to stop pointless re-renders. With it, the compiler analyses your code and inserts the equivalent caching automatically.

## Why It Matters on TV

Re-renders are expensive on a weak chip. Hand-written memoisation is easy to forget, easy to get wrong, and clutters the code. The compiler covers the cases you would have missed.

## What It Memoises Automatically

| Case | Hand-written equivalent | What the compiler does |
|---|---|---|
| Values computed during render | `useMemo` | Caches the value and recomputes only when its inputs change |
| Functions created in a component | `useCallback` | Keeps the same function reference while its inputs are unchanged |
| JSX elements | `React.memo` | Skips a child whose inputs did not change |

## What It Does Not Fix

This is the most important part for TV.

| Limitation | Why it matters |
|---|---|
| State kept too high | If focus state lives in a top-level context, the right components still have to re-render. The compiler cannot move your state. |
| Components that are slow even once | Memoisation avoids repeated work, not the first render. |

## Gotchas

| Gotcha | What to know |
|---|---|
| Relies on the Rules of React | Mutating props or state, writing to variables during render, or reading `ref.current` during render can make the compiler skip that component or produce stale output. |
| Silent skipping | When the compiler cannot prove a component is safe, it leaves it uncompiled without failing the build. You may think you are optimised when you are not. |
| Third-party code | Libraries that rely on unusual patterns or unstable references can interact badly with compiled code. |
| Harder debugging | The code that runs is not the code you wrote, and stack traces point to compiled output. |
| Cache costs memory | The cached values are kept in memory, a small cost that matters on a low-RAM TV. |
