# Microfrontend Content Loading Mechanism

## [](#%5Foverview)Overview

This document explains how Microfrontend content is loaded in the OneCX platform using Module Federation.

It helps you:

* Understand available loading approaches
* Choose the correct integration approach
* Configure microfrontends correctly

Microfrontend integration is primarily determined by two factors:

* [**Content Type**](content-type.html)  
   * Module  
   * Remote Component
* [**Expose Method**](expose-method.html)  
   * Angular  
   * Web Component

These factors depend on the type of content exposed by the microfrontend and must be configured correctly in the Application Store.

| |  **It is NOT recommended to use the Angular expose method.** Using the Angular expose method creates tight coupling between microfrontends and restricts the platform’s ability to support multiple frameworks and versions. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

| |  OneCX uses [Module Federation](https://webpack.js.org/concepts/module-federation/) with Webpack to load and expose microfrontends. |
| ------------------------------------------------------------------------------------------------------------------------------------- |

__Table 1\. Navigation__
| [← Previous: Introduction to Module Federation](../../index.html) | [Next: Content Type →](content-type.html) |
| ----------------------------------------------------------------- | ----------------------------------------- |
