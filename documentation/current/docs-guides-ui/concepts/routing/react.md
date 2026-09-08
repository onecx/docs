# Routing in React Applications

This page covers the React-specific routing guidelines. See [Routing](../routing.html) for the shared routing requirements and reasons behind them.

React applications resolve their base path at runtime using the `useAppHref` hook from `@onecx/react-webcomponents`, instead of a service injected into the router configuration.

## [](#react-useapphref)Routing with useAppHref

`useAppHref` retrieves and normalizes the URLs (base URL, app base href, and href) needed for routing in a microfrontend, relying on the `ConfigurationProvider` and `AppStateProvider` contexts from `@onecx/react-integration-interface`. Guard rendering until `href` is available, then prefix all routes with it so navigation stays aligned with the base path the shell mounted the app under.

```tsx
import { Route, Routes } from "react-router";
import { useAppHref } from "@onecx/react-webcomponents";

const AppRoutes = () => {
  const { href } = useAppHref();

  if (!href) {
    return null;
  }

  return (
    <Routes>
      <Route path={`${href}/`} element={<Overview />} />
      <Route path={`${href}/detail/:id`} element={<Detail />} />
    </Routes>
  );
};
```

See [@onecx/react-webcomponents](../../react/libraries/react-webcomponents.html) for the full library reference.
