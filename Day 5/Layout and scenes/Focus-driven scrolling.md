On TV there is no touch scrolling. The user moves focus with the D-pad, and the screen has to scroll by itself so the focused item is always visible.

When an item gets focus, check where it is. If it is outside the safe visible area (or too close to the edge), scroll so it comes back into view, and do it in a predictable position, not randomly.


There are two scroll directions:

    Direction	What scrolls	Triggered by
    Horizontal	A single rail	Left/right inside a rail
    Vertical	The whole screen (list of rails)	Up/down between rails


Some platforms already help
    tvOS and Android TV have a native focus engine, and scroll views often scroll to the focused child on their own.
    That automatic behavior is basic: it scrolls the minimum amount, so the focused card often ends up stuck against the edge with no peek of the next card.


Scroll policies
    Policy	Behavior	Feel
    Minimal	Scroll only when the item would go off-screen	Focus walks to the edge, then the list jumps. Easy but rough
    Leading edge (sticky start)	Focused item stays at the same spot (for example the left side), the list moves under it	Very stable, good for rails
    Centered	Focused item stays in the middle	Used in carousels and menus, needs padding at both ends