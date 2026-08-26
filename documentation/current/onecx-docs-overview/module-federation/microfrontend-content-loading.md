# Microfrontend Content Loading in OneCX

## [](#microfrontends-content-loading-explained)Microfrontend’s Content Loading Explained

When discussing Microfrontend loading mechanisms there are 2 important factors that decide on how loading mechanisms work. Those factors are:

* **content type**  
   * Module  
   * Remote Component
* **expose method**  
   * Angular  
   * Webcomponent

All of them are dependent on the Application Microfrontend’s content that is meant to be integrated with OneCX platform. Please make sure to properly configure each integrated Application in the Application Store.

| |  **It is NOT recommended** to use the Angular expose method. Doing so restrains the platform from using many frameworks with different versions, which means that all Microfrontends would need to use the same technology and version. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| |  OneCX platform uses **Module Federation** technology integrated with **Webpack** to expose and load Microfrontends. To find out more about how Module Federation enables Microfrontends, please refer [here](https://webpack.js.org/concepts/module-federation/). |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#content-type)Content Type

In the context of content loading, content type **determines which mechanism will be responsible for loading**. Module loading will be handled by the Shell UI router via constructed routing rules, and Remote Component loading will be handled by the Slot Component (to which the Remote Component has been assigned).

#### [](#shell-ui-router-mechanism)Shell UI Router Mechanism (Module)

When dealing with modules, Shell UI is responsible for loading them. As explained in the [Shell overview](../architecture/shell.html), Shell UI first constructs workspace and then handles routing and loading of remotes. Workspace configuration contains all valid routes to Applications registered for a given workspace, each route associated with a Microfrontend’s module.

Prior to any routing events, the Shell UI initializes the router to reflect workspace configuration. Based on the data from backend services about the current workspace, Shell UI creates routing rules to use during the runtime.

Let’s take a workspace using a User Profile Application as an example. Each Application in the workspace configuration has to have a path defined. This path is used for routing and accessing the remote entry file of the Application’s Microfrontend. Assuming the path is `/user`, Shell UI will create a routing rule specifying that whenever url of the page changes to one starting with `/user` it has to load the Microfrontend’s module.

After routing rules are successfully created, each registered Application should have a route registered in Shell UI’s router. Each route has a **loadChildren method, which is called whenever a route gets activated**, but it also has additional properties that are used by the shell during routing.

The **loadChildren method is responsible for loading the remote module into the Shell UI’s memory using [@angular-architects/module-federation](https://www.npmjs.com/package/@angular-architects/module-federation)**. When the remote module is loaded successfully, it is used by the router to display the module’s content in the content pane of the page.

#### [](#slot-component-mechanism)Slot Component Mechanism (Remote Component)

Remote Component loading is handled by the Slot Component. The overall mechanism of Remote Component loading was explained in the [Remote Components documentation](../architecture/remote-components.html). In the context of content loading, it’s important to note the following aspects:

* The Remote Component **loading process starts when a Slot Component is rendered** on a page.
* Remote Component **exposed content is loaded via [@angular-architects/module-federation](https://www.npmjs.com/package/@angular-architects/module-federation)** (similar to module content type). Then, once it’s loaded successfully, it is **rendered onto a page within the Slot Component via a dynamic content creation mechanism dependent on the chosen expose method**.

### [](#expose-method)Expose Method

Expose method is a factor that is taken into consideration by the respective loading mechanism (Shell UI router or Slot Component) to ensure correct content loading. For module loading, the loadChildren method and router configuration are impacted. For Remote Component loading, a different mechanism of dynamic content creation is chosen. For information on specific expose method impacts, please refer to the following documents:

* [Webcomponent method](webcomponents.html)

### [](#module-federation-loading-explained)Module Federation Loading Explained

Independent on the content type and expose method, OneCX platform will load exposed content using [Module Federation](https://webpack.js.org/concepts/module-federation/). During this step, exposed content is loaded using the file specified in the webpack configuration for the respective content. Such configuration is usually located in the `webpack.config.js` file. In the code snippet below, the `./src/main.ts` file would be used for the module and the `./src/app/remotes/my-comp/my-comp.component.main.ts` file for Remote Component loading.

```typescript
const config = withModuleFederationPlugin({
  name: 'my-application-ui',
  filename: 'remoteEntry.js',
  exposes: {
    './MyDefaultModule': './src/main.ts',
    './MyRemoteComponent': './src/app/remotes/my-comp/my-comp.component.main.ts'
  },
  ...
})
```

Those files should contain code that takes care of all the setup required to display the content. Depending on the chosen expose method, the code in those files will vary.

## [](#useful-resources)Useful Resources

* [Shell overview](../architecture/shell.html)
* [OneCX Microfrontend](../architecture/mfe.html)
* [OneCX Remote Components](../architecture/remote-components.html)
* [Web Components](webcomponents.html)
