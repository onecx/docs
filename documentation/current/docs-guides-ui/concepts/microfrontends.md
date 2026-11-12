# Microfrontends

A **microfrontend** is an application, or a part of one, that is developed and deployed independently and loaded into OneCX at runtime. This page is a technology-agnostic overview of the microfrontend types and loading methods in OneCX. It does not describe how to configure a microfrontend.

## [](#microfrontends-compared-to-regular-web-applications)Microfrontends compared to regular web applications

A regular web application is built and deployed as one unit and is opened on its own. A microfrontend is loaded into the OneCX Shell instead. It is developed and deployed by its own team, independently of the Shell and of other applications.

For development and deployment this means that releasing a new version of a microfrontend does not require a rebuild of the Shell. At the same time, the microfrontend must follow the platform rules described in [Required Setup](../setup/required/index.html).

## [](#types-of-microfrontends)Types of microfrontends

### [](#module)Module

A **module** is a complete web application, usually with several routes and views, that is the main content of the page. The OneCX Shell loads it and renders it in the main content area. See [Module Federation](module-federation.html) for the mechanism behind this.

### [](#remote-component)Remote component

A **remote component** is a single self-contained piece of UI that other applications can embed through a Slot. See [Remote Components](remote-components.html).

## [](#loading-methods)Loading methods

The loading method defines how the Shell loads the exposed code of a microfrontend and turns it into a web component.

### [](#webcomponentmodule)WebComponentModule

**WebComponentModule** is the loading method for microfrontends built with modern JavaScript frameworks that use ESM module loading. The exposed code is loaded as an ES module and rendered as a web component.

### [](#webcomponentscript)WebComponentScript

**WebComponentScript** is the loading method for microfrontends that do not use ESM module loading, whatever technology they are built with. The exposed code is loaded as a script and rendered as a web component.

For the difference between module and script loading, see [Module Federation remote types](https://module-federation.io/configure/remotetype#usage).

## [](#web-components-in-onecx)Web components in OneCX

Web components give a technology-agnostic way to build microfrontends and let components be reused across microfrontends. Element names must be unique across the platform, because the browser allows each name to be registered only once.

* `@onecx/angular-webcomponents` — bootstraps an Angular microfrontend as a web component. See [Angular Applications](remote-components/angular.html).
* `@onecx/react-webcomponents` — bootstraps a React microfrontend as a web component. See [@onecx/react-webcomponents](../react/libraries/react-webcomponents.html).

For details on web components, see [MDN Web components](https://developer.mozilla.org/en-US/docs/Web/API/Web%5Fcomponents).

## [](#related)Related

* [Module Federation](module-federation.html) — the mechanism that loads microfrontends into OneCX at runtime.
* [Remote Components](remote-components.html) — how a remote component is embedded into another application through a Slot.
* [Style Isolation](style-isolation.html) — how the styles of a microfrontend stay confined to the region it renders into.
* [Module Federation and Preloaders](../module-federation/mf-preloaders.html) — preloaders load before the Shell and provide the shared packages.
