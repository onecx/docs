# Module Federation Introduction

[Module Federation](https://module-federation.io/guide/start/) is a mechanism that allows code and resources to be shared across multiple JavaScript applications.

**Module Federation** is used to support a **microfrontend-based architecture** where multiple applications can work together as a single user interface.

**In OneCX**, Module Federation enables dynamic loading of UI modules, allowing applications to be developed, built, and deployed independently.

This documentation section covers module federation-related concepts, implementation details, configuration, and best practices.

Before proceeding, familiarize yourself with the following concepts:

__Table 1\. Prerequisites__
| Name                                                                                | Description                                                                                     |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [Webpack](https://webpack.js.org/concepts/)                                         | A static module bundler for **JavaScript applications** that supports Module Federation         |
| [Module Federation](https://module-federation.io/)                                  | Enables scalable, independently deployable frontend architecture with **runtime integration**   |
| [Web Components](https://developer.mozilla.org/en-US/docs/Web/API/Web%5Fcomponents) | Technology used to render applications in OneCX shell                                           |
| [Microfrontends](https://micro-frontends.org/)                                      | Extends the concepts of microservices to the frontend world                                     |
| [OneCX](https://onecx.github.io/docs/documentation/current/index.html)              | An **innovative open-source platform** solution enabling seamless **microfrontend integration** |

__Table 2\. Concepts__
| Name                                                           | Description                                                          |
| -------------------------------------------------------------- | -------------------------------------------------------------------- |
| [Microfrontend content loading](concepts/content-loading.html) | Explains how content loading is handled in OneCX                     |
| [Web Components](concepts/webcomponents/index.html)            | Explains how Web Components are used in OneCX to load Microfrontends |

__Table 3\. Microfrontends in OneCX__
| Name                                                             | Description                                                                                                                    |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| [Bootstrapping](onecx/microfrontend-bootstrapping/index.html)    | Explains how to set the initial structure and configuration for a Microfrontend application in OneCX                           |
| [Configuration](onecx/microfrontend-configuration.html)          | Explains how to configure a Microfrontend to use Module Federation for loading and dependency sharing in OneCX                 |
| [@onecx/angular-webcomponents](onecx/angular-webcomponents.html) | Explains that exposing modules and remote components via Microfrontends is the recommended approach within the OneCX platform. |
