# @onecx/angular-webcomponents Details

Using [@onecx/angular-webcomponents](#onecx/angular-webcomponents) to expose modules and Remote Components via Microfrontends is the recommended way within the OneCX platform. There are guides available that showcase how to transform already-created Microfrontend’s content to use Webcomponent method. In this section, all the specific functions available within the angular-webcomponents library are explained.

## [](#bootstrapmodule)bootstrapModule Function

Please refer to this example of [bootstrapModule](microfrontend-bootstrapping/module-bootstrapping.html#bootstrap-module). Use **bootstrapModule** function for Angular module bootstrapping.

This function ensures that the module is bootstrapped correctly and takes care of:

* ngZone sharing
* platform sharing

__Table 1\. bootstrapModule arguments__
| **Argument** | **Type**                   | **Description**                                  |
| ------------ | -------------------------- | ------------------------------------------------ |
| module       | Type<M>                    | Angular Module to load                           |
| appType      | 'shell' or 'microfrontend' | Use 'microfrontend' for exposing modules         |
| production   | boolean                    | if the application should run in production mode |

## [](#bootstrap-remote-component)bootstrapRemoteComponent Function

Please refer to this example of [bootstrapRemoteComponent](microfrontend-bootstrapping/remote-component-bootstrapping.html#bootstrap-remote-component). Use **bootstrapRemoteComponent** function for Angular Remote Component bootstrapping.

This function ensures that the Remote Component is bootstrapped correctly and takes care of:

* Remote Component router connection
* ngZone sharing
* platform sharing

__Table 2\. bootstrapRemoteComponent arguments__
| **Argument** | **Type**                                  | **Description**                                               |
| ------------ | ----------------------------------------- | ------------------------------------------------------------- |
| component    | Type<any>                                 | Angular Component to load                                     |
| elementName  | string                                    | HTML element name to be used for Custom Elements registration |
| production   | boolean                                   | if the application should run in production mode              |
| providers    | Array<(Provider \| EnvironmentProviders)> | Array of providers for Remote Component to run                |

## [](#create-app-entrypoint)createAppEntrypoint Function

Please refer to this example of [createAppEntrypoint](microfrontend-bootstrapping/module-bootstrapping.html#module-bootstrapping-example). Use **createAppEntrypoint** function to create an entrypoint component for Microfrontend’s module in the Microfrontend’s ngDoBootstrap function.

__Table 3\. createAppEntrypoint arguments__
| **Argument** | **Type**  | **Description**                                                                                                                                         |
| ------------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| component    | Type<any> | Angular Component to load, representing module entrypoint. This component should have **router-outlet** in its template to enable routing for a module. |
| elementName  | string    | HTML element name to be used for Custom Element’s registration of entrypoint                                                                            |
| injector     | Injector  | Module’s injector (usually this.injector) to be used for dependency injection                                                                           |

## [](#initialize-router)initializeRouter Function

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

## [](#starts-with)startsWith Function

Please refer to this example of [startsWith](microfrontend-bootstrapping/module-bootstrapping.html#module-bootstrapping-example). Use **startsWith** function when constructing Routes for Microfrontend’s module.

__Table 4\. createAppEntrypoint arguments__
| **Argument** | **Type** | **Description**                                             |
| ------------ | -------- | ----------------------------------------------------------- |
| prefix       | string   | Prefix to match in order to display certain module content. |

__Table 5\. Navigation__
| [← Back to Module federation bootstrapping and configuration in OneCX](index.html) |
| ---------------------------------------------------------------------------------- |
