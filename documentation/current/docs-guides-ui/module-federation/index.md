# Module Federation in OneCX

**Module Federation** is a Webpack feature that enables the dynamic loading of separately built and deployed **JavaScript applications**.

In **OneCX**, it enables different applications **microfrontends** to be developed, built and deployed independently while still sharing code and dependencies at **runtime**.

This guide introduces module federation in **OneCX**, explains how to use and configure it in your applications.

## [](#prerequisites)Prerequisites

Before visiting this guide, let’s visit following concepts:

__Table 1\. Concepts__
| Name                                                                               | Description                                                                                      |
| ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| [Webpack](https://webpack.js.org/concepts/)                                        | Static module bundler for **JavaScript applications** that supports module federation            |
| [Module Federation](https://module-federation.io/)                                 | Enables scalable, independently deployable frontend architecture with **runtime integration**    |
| [Webcomponents](https://developer.mozilla.org/en-US/docs/Web/API/Web%5Fcomponents) | Technology used to render applications in OneCX shell                                            |
| [Microfrontends](https://micro-frontends.org/)                                     | Extends the concepts of micro services to the frontend world                                     |
| [OneCX](https://onecx.github.io/docs/documentation/current/index.html)             | An **innovative open-source platform** solution enabling seamless **microfrontends integration** |
| [Types of Microfrontends in OneCX](types-of-microfrontends.html)                   | WebComponentModule, WebComponent script, webcomponent and Angular microfrontends                 |

## [](#usage-of-module-federation-in-onecx)Usage of Module Federation in OneCX

In OneCX, **Module Federation** is used to load microfrontends, expose reusable components, and for dependency sharing.

Following are important concepts where module federation is involved:

__Table 2\. Features__
| Name                                                            | Description                                           |
| --------------------------------------------------------------- | ----------------------------------------------------- |
| [Preloaders](mf-preloaders.html)                                | Preloaders register Module Federation share scopes    |
| [Shell router](mf-shell-router.html)                            | Shell router - dynamic content loading                |
| [Dependency Sharing](mf-dependancy-sharing.html)                | Build-time and runtime negotiation of shared packages |
| [Slot components](mf-slot-components.html)                      | Load remote modules or components in slots            |
| [Custom Authentication Service](mf-authentication-service.html) | Implementation of a custom authentication service     |

## [](#onecx-recommendations)OneCX Recommendations

The following documents describe how to configure and use Module Federation in OneCX.

| Name                                                             | Description                                                                |
| ---------------------------------------------------------------- | -------------------------------------------------------------------------- |
| [Module federation configuration](module-federation-config.html) | Describes how to configure module federation in microfrontends             |
| [Application bootstrapping](application-bootstrapping.html)      | Describes how to bootstrap microfrontends content to use module federation |
