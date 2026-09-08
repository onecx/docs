# Expose Library Assets in React Applications

This page covers exposing the static assets of the OneCX libraries a React application depends on. See [Expose Library Assets](../expose-library-assets.html) for why this matters.

The end goal for React applications is the same as for any other technology: the static assets (e.g. icons) shipped by the OneCX libraries depended on must be exposed in the application’s own build output, since Micro Frontends are loaded relative to the shell rather than from their own origin.

Translation files are resolved for React applications at runtime — see [@onecx/react-utils: Translation Resource Registration](../../../react/libraries/react-utils.html#translation-resources) for that mechanism. There is currently no equivalent OneCX-prescribed build-time mechanism documented for exposing other library assets (e.g. icons) in React applications. Until such a mechanism is documented, confirm what assets the OneCX libraries in use ship, and ensure the build makes them available in the build output at a path the application resolves them from.

See [@onecx/react-utils](../../../react/libraries/react-utils.html) for the library reference of the runtime helpers React applications rely on.
