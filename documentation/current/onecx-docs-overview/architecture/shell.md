# OneCX Shell

## [](#overview)Overview

OneCX Shell is the heart of the OneCX platform. It’s the most important OneCX core Application that glues together all Applications and makes the platform seem like a single page application. Without the Shell running, there will be nothing for users to use.

## [](#application-bundle)Application Bundle

Below is a list of apps the Shell Application consists of:

* UI - user interface app which renders the platform overlay and is responsible for routing between applications
* BFF - backend for frontend app connecting with OneCX core applications SVCs to construct workspaces

## [](#application-responsibilities)Application Responsibilities

The Shell Application is a special case of OneCX Application. It is a host for Microfrontends within the platform. The list of its responsibilities is the following:

* client-side workspace construction
* routing and remotes loading
* workspace and user data sharing

### [](#client-side-workspace-construction)Client-side Workspace Construction

OneCX platform is operating on the idea of workspaces. Each workspace can have many applications registered and can be customized to its users' needs via custom menu configuration, page theming and many more possibilities. To construct a valid workspace, the following operations happen:

1. **Shell BFF gathers workspace information**. Data required to construct a valid workspace to function on the platform is saved in several databases. These can be reached using the backend services of OneCX Core Applications. Shell BFF connects with them and gathers all required information in a single response.
2. **Shell UI constructs routing rules** for a given workspace based on the data fetched by Shell BFF.

### [](#routing-and-loading-remote-modules)Routing and Loading Remote Modules

When Shell UI is finished with workspace construction, its next responsibility is to **react to routing changes and load Microfrontends' exposed modules** into the page. To achieve that, Shell UI App is using [@angular-architects/module-federation](https://www.npmjs.com/package/@angular-architects/module-federation), which allows loading remote entries at runtime. In this way, on a valid routing operation, the Shell UI App will load the exposed Microfrontend’s module and display it in the content pane of the page.

| |  Shell is responsible for loading Microfrontend’s modules only. To learn more, please refer to the [Microfrontend content loading document](../module-federation/microfrontend-content-loading.html). |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#workspace-and-user-data-sharing)Workspace and User Data Sharing

When Shell UI App receives the workspace and current user data from the backend, it makes sure that this data is available for any Microfrontend’s content. This data is passed on by the Shell UI App to Topics.

A Topic is a similar concept to an Observable, but it can be used to pass data between the UI Apps using browser memory. It is a concept implemented in OneCX. A more in-depth explanation of it can be found here. For Angular-based Microfrontends, services in the [@onecx/angular-integration-interface](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html) package might be useful during the development. They are operating on [Topics](../../onecx-portal-ui-libs/libraries/integration-interface.html#topics) that contain information passed along by the Shell UI App.

Having data in browser memory via [Topics](../../onecx-portal-ui-libs/libraries/integration-interface.html#topics) gives Microfrontend’s content direct access to information about the workspace and current user. Information passed on by the Shell UI App contains the following information:

* details of current workspace
* Remote Components and Slots registered for the current workspace
* the current user’s personal information, settings (such as language or locale), permissions
* currently accessed Application data (information available after Application’s Microfrontend gets loaded)

Any Microfrontend’s content can then utilize this data and act on it with the possibility to react to data changes.

## [](#useful-resources)Useful Resources

* [Architecture Overview](index.html)
* [Microfrontends in OneCX](mfe.html)
* [Remote Components in OneCX](remote-components.html)
* [@onecx/integration-interface](../../onecx-portal-ui-libs/libraries/integration-interface.html)
* [@onecx/angular-integration-interface](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html)
* [Webpack Module Federation](https://webpack.js.org/concepts/module-federation/)
