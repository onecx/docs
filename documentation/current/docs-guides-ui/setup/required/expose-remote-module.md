# Expose a Remote Module

Every application integrated with OneCX must expose itself to the shell via Module Federation, so the shell can dynamically load it at runtime. This page covers the requirements and setup steps for both Angular and React applications.

## [](#overview)Overview

Content loading is triggered by route changes (for modules) or Slot Component display (for remote components). The content is loaded via Module Federation configuration exposed by the application. The recommended setup uses `@module-federation/enhanced` and exposes `mf-manifest.json`; `remoteEntry.js` is still supported when the shell configuration points directly to it. See [Platform & Package Compatibility Requirements](platform-package-compatibility.html) for the full compatibility baseline.

`mf-manifest.json` contains metadata about the exposed modules and their dependencies and enables better integration and compatibility with the shell. See [Exposing mf-manifest.json file](../../../onecx-docs-dev/shell-integration/shell-v3-migration.html#mf-manifest) for details.

## [](#angular-applications)Angular Applications

### [](#angular-webcomponent-method)Webcomponent Method (Recommended)

This method uses Web Components **Custom Elements** to register content, allowing multiple frameworks and Angular versions to coexist in the shell. It is the recommended approach; the alternative "Angular expose method" (exposing an `NgModule` directly) limits the whole platform to a single Angular version and is not recommended.

There are two ways to expose an Angular application depending on what needs to be loaded by the shell:

* [Module Approach](expose-remote-module/module-approach.html) — expose a full Angular module, loaded on route activation.
* [Component Approach](expose-remote-module/component-approach.html) — expose a single component, loaded by a Slot Component.

## [](#react-applications)React Applications

React applications are turned into a Custom Element and exposed the same way, using `@onecx/react-webcomponents`.

### [](#react-vite-webcomponent)Converting a React App into a Web Component

The `createViteAppWebComponent` function converts a React component or React app into a custom web component, relying on the browser’s Custom Elements API and the `@r2wc/react-to-web-component` library.

```js
const createViteAppWebComponent = (
  app: React.ComponentType,
  elementName: string
) => {
  // Implementation
};
```

* `app`: the React component to convert into a web component.
* `elementName`: the name of the custom element to register (e.g. `my-custom-element`).

Example for a Vite App

```js
import App from './app';
import { createViteAppWebComponent } from '@onecx/react-webcomponents';

createViteAppWebComponent(App, 'my-custom-app');
```

Expose the resulting entry point through the Module Federation configuration:

```js
const config = withModuleFederationPlugin({
  name: 'example-react-ui',
  filename: 'remoteEntry.js',
  exposes: {
    './ExampleApp': './src/main.tsx'
  },
})
```

See [@onecx/react-webcomponents](../../react/libraries/react-webcomponents.html) for the full library reference, including routing helpers (`useAppHref`, `SyncedRouterProvider`) used once the app is loaded in the shell.
