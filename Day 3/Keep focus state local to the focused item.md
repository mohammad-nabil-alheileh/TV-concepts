# Keep Focus State Local to the Focused Item

When focus moves, only the two items involved should re-render: the one losing focus and the one gaining it.

## Why It Matters on TV

Focus changes constantly. Users hold the D-pad and cross dozens of items per second. Re-rendering one screen's worth of cards on every press is the difference between a smooth highlight and visible lag on a weak TV chip.

## Expected Re-renders on a Focus Move

| Item | Should re-render? | Reason |
|---|---|---|
| Item losing focus | Yes | It needs to remove its highlight |
| Item gaining focus | Yes | It needs to show its highlight |
| All other items in the rail or screen | No | Their focus state has not changed |
| Parent screen or container | No | Focus state should not live here |

## When the Parent Needs to Know What Is Focused

If a parent genuinely needs to know what is focused, do not put that value in state that wraps everything. Use one of these options instead:

| Option | How it works | Trade-off |
|---|---|---|
| Lift state into a small, separate component | Only the component that needs the focused item subscribes to the value | Simple, but the state must be placed carefully |
| Use a store with selectors | Components subscribe only to the slice they read, so only the banner re-renders | Adds a store dependency |
| Debounce the update | Fast scrolling does not trigger a banner change on every card | Updates are slightly delayed |
