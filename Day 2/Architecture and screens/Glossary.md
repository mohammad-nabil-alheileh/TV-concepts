Component: A reusable piece of UI, such as a button, a card or a row of posters. It knows nothing about navigation.

Screen: A full-page view the user navigates to, such as Home, Player or Settings. It is built from components and usually owns its data loading and its initial focus.

Route: The name (and params) that identifies a screen in the navigator. It’s the address, while the screen is the content at that address.

Overlay: UI drawn on top of the current screen without leaving it, such as a modal, a “Are you sure?” dialog or the player controls. It is not a route, so the screen underneath stays mounted.