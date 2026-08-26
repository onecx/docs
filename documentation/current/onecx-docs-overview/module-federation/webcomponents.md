# Web Components in OneCX

## [](#overview)Overview

Web Components is a suite of different technologies used to create reusable custom elements with encapsulated functionality. In the OneCX context, they are useful for dynamic content creation for both modules and the display of Remote Components in Microfrontends. Prior to reading this document, it is recommended to read the documentation of [microfrontend content loading](microfrontend-content-loading.html) to get familiar with the content loading mechanisms available within the OneCX platform.

| |  Webcomponent expose method enables the OneCX platform to use UI Apps developed with different frameworks and versions. It is the **recommended method for all Applications**. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| |  Web Components technologies are used within OneCX platform. However, OneCX offers its own functionalities that should be used to expose Microfrontend’s content using the Webcomponent expose method. Those functionalities are based on Web Components technologies, so there is no need to get familiar with them. Nevertheless, more resources about Web Components can be found [here](https://developer.mozilla.org/en-US/docs/Web/API/Web%5Fcomponents) |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#web-components-preview)Web Components Preview

Web Components are used in OneCX context for dynamic content creation. OneCX platform uses Web Components technologies to bound UI components to HTML elements. OneCX platform will use information from the Application Store to determine what HTML elements have to be rendered to allow certain modules and Remote Components to be bound to page content.

With Webcomponent expose method, the OneCX platform is only loading the code required for Microfrontend’s content into the Shell UI memory and creating a "host" element for Remote Components or modules to attach to using Web Components. The Microfrontend’s exposed content is partially responsible for the content creation. Microfrontends have to adapt exposed modules and components, so they are using Web Components Custom Elements.

### [](#custom-elements)Custom Elements

Custom Elements are part of the Web Components technology. It is a set of tools used to achieve the bounding between components and HTML elements. As mentioned, OneCX platform will create HTML elements specified via configuration whenever a module or Remote Component has to be displayed on a page. There are 2 steps that OneCX platform takes when dealing with content loading with Webcomponent expose method:

1. Load exposed content via Module Federation into memory.
2. Create an HTML element on a page to which exposed content should be bound.

In the [Microfrontend content loading](microfrontend-content-loading.html#module-federation-loading-explained), it was mentioned that when exposing Microfrontend content, files specified per content should take care of all setup needed to display it. With Webcomponent method, those files need to contain source code, which will register the Custom Element in the Custom Elements Registry. Without getting into the details of Web Components, a file used for content loading needs to use Web Components to assign some component to the HTML element that OneCX platform will render. This way, when OneCX platform creates this HTML element on a page, the Custom Elements Registry will use the assigned component and display it on a page.

### [](#webcomponent-expose-method-requirements)Webcomponent Expose Method Requirements

To correctly use Webcomponent expose method, 2 requirements need to be fullfield:

1. Database is correctly configured for module or Remote Component  
   1. **technology** set to **WebComponent**  
   2. **tag name** set to agreed **HTML element name**
2. Microfrontend is adapted to expose Web Components compliant content  
   1. desired component needs to be registered as Custom Element in the Custom Elements Registry  
   2. Angular issues are covered (use the `[@onecx/angular-webcomponents](#onecx/angular-webcomponents)` library to cover them by default)  
         1. multiple routers synchronization  
         2. ngZone sharing  
         3. platform sharing

| |  Database configuration is easy to set up using the Application Store Application. |
| ------------------------------------------------------------------------------------ |

| |  To ensure Microfrontend compliance with Web Components for Angular modules and Remote Components, it is recommended to use the **[@onecx/angular-webcomponents](#onecx/angular-webcomponents)** library. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#expose-microfrontends-content-as-web-components)Expose Microfrontend’s Content as Web Components

OneCX platform offers different ways of [exposing Microfrontend’s content](../architecture/mfe.html). One of them is **Webcomponent method**.

When exposing content with Webcomponent method, it is required to ensure the correct setup. For exposing Angular content, there are functionalities provided via the [@onecx/angular-webcomponents](#onecx/angular-webcomponents) library. For a detailed guide on how to expose Microfrontend’s content via Webcomponent method, please refer here.

| |  Using **[@onecx/angular-webcomponents](#onecx/angular-webcomponents)** library, according to the guide, is the recommended way of exposing Angular content. The set of functionalities provided via the library is taking care of all requirements related to the Web Components adaptation. Apart from automatic registration to the Custom Elements Registry, they ensure that the following issues are covered: Every module and Remote Component is going to have its own router. Routers (Shell’s router, displayed module’s router, and router of each displayed Remote Component) need to be synchronized so each can react to the router events. A Single Angular version can only create one platform to operate on, which means that for every content loaded within a page, the same platform has to be used for a specific version. ngZone of Shell UI has to be shared with all modules and Remote Components to allow Web Components to function correctly. In-depth explanations for those issues can be found in the [Module Federation multi-framework and version micro frontends document](https://www.angulararchitects.io/en/blog/multi-framework-and-version-micro-frontends-with-module-federation-the-good-the-bad-the-ugly/). |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#onecx-adaptation-to-webcomponent-method)OneCX Adaptation to Webcomponent Method

As stated in [Microfrontend content loading documentation](microfrontend-content-loading.html), every method of Microfrontend’s content exposal has an impact on the OneCX platform behavior for both module and Remote Component loading. The adaptations made by OneCX to work with Web Components were briefly mentioned in the Web Components preview, however depending on the content type, the behavior varies.

### [](#module-loading-behavior)Module Loading Behavior

The Shell UI App is responsible for displaying Microfrontend’s module when router navigation is matched for a desired Microfrontend. With Webcomponent method, Shell UI will adapt the loadChildren method to:

1. load desired remote module using [@angular-architects/module-federation](https://www.npmjs.com/package/@angular-architects/module-federation) (no change).
2. use **WebComponentLoaderModule** as the module to be lazy-loaded (instead of the Microfrontend’s module).

The [loadChildren method bound to a Route](https://angular.dev/guide/ngmodules/lazy-loading) is an asynchronous method that in the end should return a module to be displayed when activating a certain Route. With Webcomponent method, the desired Microfrontend’s module is still being loaded using [@angular-architects/module-federation](https://www.npmjs.com/package/@angular-architects/module-federation). During that loading, it should register a component in the Custom Elements Registry, as mentioned in the previous section. For OneCX platform, it means that it no longer should load the Microfrontend’s module directly but ensure that the HTML code has the correct Custom Element in order to display the module.

**WebComponentLoaderModule** is a simple Angular module with a Router set up to always display **WebComponentLoaderComponent**. This component is responsible for rendering the HTML element required to display the module with Web Components Custom Elements. Whenever Shell UI’s router detects a change of the Microfrontend (another path is matched than the current one), it calls **loadChildren method** to load the desired module and returns **WebComponentLoaderModule**. The module then creates and initializes **WebComponentLoaderComponent**, which, after initializations, creates the HTML element. Then Web Components using Custom Elements technology bounds the Microfrontend’s module to the created element.

For a detailed guide on how to expose Microfrontend’s module via Webcomponent method, please refer here.

### [](#remote-component-behavior)Remote Component Behavior

Slot Component is responsible for displaying Microfrontend’s Remote Components during Slot Component initialization. With the Webcomponent method, the Slot Component will adapt the steps to:

1. load desired remote content using [@angular-architects/module-federation](https://www.npmjs.com/package/@angular-architects/module-federation) (no change).
2. create HTML element directly inside a container (instead of creating Microfrontend’s Remote Component instance).

The Slot Component content is based on [Angular ViewContainerRef](https://angular.dev/api/core/ViewContainerRef) to dynamically create content inside the Slot Component. With Webcomponent method, the desired Microfrontend’s Remote Component is still being loaded using [@angular-architects/module-federation](https://www.npmjs.com/package/@angular-architects/module-federation). During that loading, it should register a component in the Custom Elements Registry, as mentioned in the previous section. For OneCX platform, it means that it no longer should create the Microfrontend’s component directly but ensure that the HTML code has the correct element in order to display the component.

The difference with the Webcomponent method is that, from the OneCX platform’s perspective, no component needs to be created. Instead, a "host" element must be created to allow Web Components' Custom Elements to display desired content.

For a detailed guide on how to expose Microfrontend’s Remote Components via Webcomponent method, please refer here.

## [](#onecx-angular-webcomponents)@onecx/angular-webcomponents Details

Using [@onecx/angular-webcomponents](#onecx/angular-webcomponents) to expose modules and Remote Components via Microfrontends is the recommended way within the OneCX platform. There are guides available that showcase how to transform already-created Microfrontend’s content to use Webcomponent method. In this section, all the specific functions available within the angular-webcomponents library are explained.

### [](#bootstrapmodule)bootstrapModule Function

Use **bootstrapModule** function for Angular module bootstrapping.

This function ensures that the module is bootstrapped correctly and takes care of:

* ngZone sharing
* platform sharing

__Table 1\. bootstrapModule arguments__
| **Argument** | **Type**                   | **Description**                              |
| ------------ | -------------------------- | -------------------------------------------- |
| module       | Type<M>                    | Angular Module to load                       |
| appType      | 'shell' or 'microfrontend' | Use 'microfrontend' for exposing modules     |
| production   | boolean                    | if application should run in production mode |

### [](#bootstrap-remote-component)bootstrapRemoteComponent Function

Use **bootstrapRemoteComponent** function for Angular Remote Component bootstrapping.

This function ensures that the Remote Component is bootstrapped correctly and takes care of:

* Remote Component router connection
* ngZone sharing
* platform sharing

__Table 2\. bootstrapRemoteComponent arguments__
| **Argument** | **Type**                                  | **Description**                                               |
| ------------ | ----------------------------------------- | ------------------------------------------------------------- |
| component    | Type<any>                                 | Angular Component to load                                     |
| elementName  | string                                    | HTML element name to be used for Custom Elements registration |
| production   | boolean                                   | if application should run in production mode                  |
| providers    | Array<(Provider \| EnvironmentProviders)> | Array of providers for Remote Component to run                |

### [](#create-app-entrypoint)createAppEntrypoint Function

Use **createAppEntrypoint** function to create an entrypoint component for Microfrontend’s module in the Microfrontend’s ngDoBootstrap function.

__Table 3\. createAppEntrypoint arguments__
| **Argument** | **Type**  | **Description**                                                                                                                                         |
| ------------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| component    | Type<any> | Angular Component to load, representing module entrypoint. This component should have **router-outlet** in its template to enable routing for a module. |
| elementName  | string    | HTML element name to be used for Custom Element’s registration of entrypoint                                                                            |
| injector     | Injector  | Module’s injector (usually this.injector) to be used for dependency injection                                                                           |

### [](#initialize-router)initializeRouter Function

Use **initializeRouter** function as APP\_INITIALIZER in the Microfrontend’s module definition.

This function ensures that the bootstrapped module’s router is connected with other routers.

```typescript
@NgModule({
  ...
  providers: [
    {
      provide: APP_INITIALIZER,
      useFactory: initializeRouter,
      multi: true,
      deps: [Router, AppStateService]
    }
  ]
})
export class RemoteModule ...
```

### [](#starts-with)startsWith Function

Use **startsWith** function when constructing Routes for Microfrontend’s module.

__Table 4\. createAppEntrypoint arguments__
| **Argument** | **Type** | **Description**                                             |
| ------------ | -------- | ----------------------------------------------------------- |
| prefix       | string   | Prefix to match in order to display certain module content. |

## [](#useful-resources)Useful Resources

* [Microfrontend Content Loading](microfrontend-content-loading.html)
* Remote Component with Webcomponent method integration
* Module with Webcomponent method integration
