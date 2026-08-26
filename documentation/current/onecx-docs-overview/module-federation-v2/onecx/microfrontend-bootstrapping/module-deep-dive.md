# Remote Module Example Deep Dive

The **module.ts** file prepares the module for integration with the OneCX platform.

This example showcases the recommended approach of defining modules (Angular-based) using the Webcomponent method. Here is a list of important features of this example:

Module imports

* CommonModule, BrowserModule and BrowserAnimationsModule Angular modules used for adding functionality to the module.
* PortalCoreModule is defined to allow usage of OneCX components and services.
* TranslateModule is defined to allow translations using translation keys within the module.
* AngularAuthModule is defined to use OneCX authorization mechanisms.
* RouterModule is defined for routing to feature modules within the exposed module.

Entrypoint component

AppEntrypoint is a standard Angular component that has a `<router-outlet>` element in its template. The [createAppEntrypoint](../angular-webcomponents.html#create-app-entrypoint) registers AppEntrypointComponent in the Custom Elements Registry, so anytime '<example-webcomponent>' is rendered, AppEntrypointComponent should be instantiated.

The third parameter, being the module’s Injector, is very important. This injector will be used by the instances of AppEntrypointComponent rendered using Web Components technology, meaning that each instance will have everything related to the module already set up. That also means the `<router-outlet>` will be using routes defined for the module.

The [createAppEntrypoint](../angular-webcomponents.html#create-app-entrypoint) method is also responsible for connecting the module’s router to the Shell’s router. Every time the URL of the browser changes, the Shell is going to publish a new message, via [EventsTopic](../../../../onecx-portal-ui-libs/libraries/integration-interface.html#events-topic), with information about the new URL. The `createAppEntrypoint` method subscribes to the [EventsTopic](../../../../onecx-portal-ui-libs/libraries/integration-interface.html#events-topic) and updates the router state accordingly to the received information.

| |  For technologies other than Angular, it is recommended to: register a Custom Element in the Custom Elements Registry. provide dependencies to registered Custom Element according to the module. listen to [EventsTopic](../../../../onecx-portal-ui-libs/libraries/integration-interface.html#events-topic) data changes and update the state of the module’s routing. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Routes matching

Each defined route will load a feature module whenever it is activated. Because the Webcomponent expose method causes multiple routers to exist at the same time (Shell has its own router and every module or Remote Component displayed at a single point in time can have their own), an adjustment to the routes definition has to be made.

The idea of routing in this example is the following:

* User enters 'shell\_url/workspace\_name/example\_base\_path' URL - FeatureModule is used.
* User enters 'shell\_url/workspace\_name/example\_base\_path/tracking' URL - TrackingModule is used.

With the following URL parts meaning:

* `shell_url` \- the Shell Application deployment URL, e.g. `localhost:4200/shell.`
* `workspace_name` \- name of the accessed Workspace, e.g. `admin`.
* `example_base_path` \- base path of the example Microfrontend (configured via OneCX Core Applications), e.g. `example`.

Prior to routing within Microfrontend’s module, the Shell uses shell\_url, workspace\_name and example\_base\_path parts of the URL to load the module. Because of this fact, the module’s router needs to remove those parts from consideration when matching its routes. Usually, the `path` property of the route is used to control the route activation, but in that case, the Microfrontend’s module needs a way to only match the relevant part of the URL.

Using the [startsWith](../angular-webcomponents.html#starts-with) function from [@onecx/angular-webcomponents](../angular-webcomponents.html#onecx-angular-webcomponents) for the [matcher](https://angular.dev/api/router/UrlMatcher) property of a route object results in the router considering only those URL parts relevant to the module. In order for it to work properly, the [initializeRouter](../angular-webcomponents.html#initialize-router) provider has to be added for the module as an app initializer.

During module creation [initializeRouter](../angular-webcomponents.html#initialize-router):

* adds Microfrontend information (based on [CurrentMfeTopic](../../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-mfe-topic)) to each route.
* rewrites routes containing `redirectTo` for correct redirection.
* creates a new route (used when routing away from the module):  
   * matched when none of the defined routes were matched.  
   * displays nothing (for a period of time when the user routes between Microfrontends).

The [startsWith](../angular-webcomponents.html#starts-with) method uses Microfrontend information, saved in the route’s data, to remove already used parts from consideration when matching routes within the module.

To create your own matchers, please consider using the [@onecx/angular-webcomponents](../angular-webcomponents.html#onecx-angular-webcomponents) library.

| |  For technologies other than Angular, it is recommended to: Use Microfrontend information from [CurrentMfeTopic](../../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-mfe-topic) to only use relevant parts of the URL for routing and redirecting correctly. Ensure routing away from the module is not causing side effects. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Configuration

All services utilizing HttpClient used within the Microfrontend’s module need to know how to make requests to external resources. Depending on the configuration of the Workspace, they need to take that context into consideration when creating a URL for those resources.

A service might want to call `deployment_url/bff/search` by default. With this call being made, the MFE App will need to access the BFF. When the Application’s path within the Workspace is `mfe/example` the call has to be made to `deployment_url/mfe/example/bff/search`.

The `apiConfigProvider` presented in the example is utilizing the `PortalApiConfiguration` class as `Configuration` for the services. It is listening for the [CurrentMfeTopic](../../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-mfe-topic) changes and overwriting the basePath accordingly to the received message, and all services use that information to construct a valid URL.

| |  For technologies other than Angular, it is recommended to: Listen to [CurrentMfeTopic](../../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-mfe-topic) changes and overwrite services configuration to ensure the correct resource is accessed. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

__Table 1\. Navigation__
| [← Previous: Module Bootstrapping and Configuration](module-bootstrapping.html) | [Next: Back to Microfrontend Bootstrapping →](../../../index.html) |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
