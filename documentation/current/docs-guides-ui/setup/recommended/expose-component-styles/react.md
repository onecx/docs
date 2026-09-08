# Expose Component Styles in React Applications

This page covers exposing a React application’s styles in the build output. See [Expose Component Styles](../expose-component-styles.html) for why this matters.

## [](#react-expose-app-styles)Expose App styles.css

The goal for React applications is the same as for any other technology: expose a stable `styles.css` file, containing the app’s styles, in the build output so the shell can style the app correctly. There is no single OneCX-prescribed mechanism for React — how this is achieved depends on the build tool used (e.g. Vite, webpack).

As general guidance:

* Configure the build so all of the application’s styles are emitted into a single stylesheet.
* Because the generated stylesheet filename often includes a content hash, adjust the build output (e.g. via a post-build step) so a stable `styles.css` file is available.
* Verify that `styles.css`, including all of the app’s styles, is present in the build output before deploying.

| |  This page does not cover style scoping (isolating the app’s styles from other applications in the shell). See [@onecx/react-utils](../../../react/libraries/react-utils.html) for the style scoping helpers provided for React applications. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
