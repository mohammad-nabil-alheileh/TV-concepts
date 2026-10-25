# Caching and Prefetch

The user should never wait for data they could already have.

There are two ways to achieve this:

1. Stale-while-revalidate
2. Prefetch when focus rests

## a) Stale-While-Revalidate

**The rule:** show cached data immediately, even if it may be old, then fetch fresh data in the background and swap it in. The user sees content instantly and still ends up with up-to-date data.

### Two Timers Control the Behavior

| Timer | Meaning |
|---|---|
| Freshness window | How long data counts as fresh. While fresh, no refetch happens at all. |
| Garbage time | How long unused data stays in memory before it is thrown away. |

### Decisions to Make

| Question | Answer / Action |
|---|---|
| Which data can be stale? | A movie catalogue, yes. A bank balance, no. |
| What happens when revalidation fails offline? | Keep showing the cache. |
| What happens after a mutation (like adding a favourite)? | Invalidate the related queries so they refetch. |

## b) Prefetch When Focus Rests

Prefetching means loading data before the user asks for it.

This is most important on TV, where users move through tiles with a D-pad. Focus passes over many items quickly, so prefetching on every focus would flood the network. Prefetching only after focus rests for about **300 ms** catches the item the user is actually considering.

### Prefetch Budget

- Also prefetch **images**, not just JSON.
- Cap the number of concurrent prefetches.
- Consider skipping prefetch on slow or metered connections.
