# Remote Component Example Deep Dive

The **example.component.ts** file prepares the Remote Component for integration with the OneCX platform.

This example showcases the recommended approach to define Remote Components (Angular-based) using the Webcomponent method. Here is a list of important features of this example:

Component bootstrap

Remote Components are better suited for integration with the Web Components Custom Elements concept. The biggest reason for this is that a Remote Component already represents a component, meaning that there is no need to define any additional entry point component (like what was done for module content type).

The [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component) method is bootstrapping the Remote Component. It is responsible for:

Creating application

As a first step, the [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component) method is going to create an Angular application. The created application will use defined providers (argument of [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component)). In this example, the following providers are defined:

* HttpClient (via provideHttpClient) - used for making HTTP calls.
* TranslateService (via provideTranslateServiceForRoot) - used for making translations via translation keys.
* providers from AngularAuthModule - OneCX authorization mechanisms.
* providers from BrowserModule.
* providers from BrowserAnimationsModule.
* APP\_INITIALIZER using userProfileInitializer factory function - in ExampleComponent’s constructor, the `this.userService.lang$.getValue()` call is made to set TranslationService language. Since that call is synchronous, it is important to ensure that [UserService](../../../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#user-service) has been initialized before fetching its data.

| |  Providers passed in the xref:module-federation-v2/onecx/angular-webcomponents.adoc#bootstrap-remote-componentbootstrapRemoteComponent method call should contain any providers required by the Remote Component. Any services or injection tokens have to be defined here. It is important that those providers are aligned with imports defined via the Remote Component’s definition. Depending on the Remote Component, different providers and imports will be defined. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

The created application is going to have an Injector (just like a module does). This Injector will be used by the instance of ExampleComponent rendered using Web Components technology.

For Angular-based Remote Components, it is recommended to use [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component) and define every required provider as an argument of this method. This approach will ensure that the rendered component has all required services, tokens, etc. already set up.

Fixing [Angular issues](../../concepts/webcomponents/expose-content-as-webcomponent.html#angular%5Fissues) (Angular requirement only)

The [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component) method takes care of ngZone and platform sharing.

Connecting router

The [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component) method is responsible for connecting the Remote Component’s router to the Shell’s router (if there is one defined), so their states are always the same. The connection is set up in the same way as for the [module’s router](#module-rotuer-connection).

Registering the Custom Element

The [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component) method registers the ExampleComponent in the Custom Elements Registry, so anytime `<example-remote-component>` is rendered, ExampleComponent should be instantiated.

| |  For technologies other than Angular, it is recommended to: register a Custom Element in the Custom Elements Registry. provide dependencies to registered Custom Element according to the Remote Component. listen for EventsTopic data changes and update the state of the Remote Component’s routing (if routing is used). |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Component definition and configuration

For Angular-based components, any Remote Component is required to be a standalone Angular component. The component’s import array’s purpose is to declare all required dependencies, just like for Angular modules. It is recommended to import:

* AngularAuthModule for authorization mechanisms.
* CommonModule for common Angular functionalities.
* SharedModule with `PortalCoreModule.forMicroFrontend()` import for allowing OneCX components and services usage.
* PortalCoreModule so the component recognizes OneCX components and services.
* TranslateModule for translations mechanism.
* AngularRemoteComponentsModule.

In the **example.component.bootstrap.ts**, some providers related to those dependencies were already declared in the [bootstrapRemoteComponent](../angular-webcomponents.html#bootstrap-remote-component) method call.

| |  For technologies other than Angular, it is recommended to: define the component so that all dependencies are provided. |
| ------------------------------------------------------------------------------------------------------------------------- |

Configuration and initialization

The ExampleComponent implements two interfaces:

* ocxRemoteComponent - requires component to define ocxInitRemoteComponent method
* ocxRemoteWebcomponent - requires component to define ocxRemoteComponentConfig property

For Webcomponent method, it is required to implement ocxRemoteWebcomponent, but optional to implement ocxRemoteComponent. The `ocxRemoteComponentConfig` is set by the Remote Component’s Slot Component after the Remote Component’s element is created in the HTML. The value that is set is of type [RemoteComponentConfig structure](#RemoteComponentConfig). On receiving the configuration, the Remote Component should:

* update BASE\_URL.
* update permissions (if permissions are used).
* update the base URL of its services (if services that require external calls are used).

__Table 1\. RemoteComponentConfig structure__
| **Property** | **Type**   | **Description**                                                                                                                         |
| ------------ | ---------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| appId        | string     | Unique identifier of the Microfrontend Remote Component is part of.                                                                     |
| productName  | string     | Name of the Application currently Remote Component is part of.                                                                          |
| permissions  | string\[\] | Current user permissions related to the Remote Component’s Microfrontend.                                                               |
| baseUrl      | string     | URL of Remote Component’s Microfrontend to be used when accessing its content (remote entry file, assets, etc.), e.g. '/mfe/mfe\_name'. |

| |  For technologies other than Angular, it is recommended to: implement the component so the ocxRemoteComponentConfig property is defined, and whenever it is set: the component’s resources or the component itself will use the correct baseUrl to access external resources. permission checking mechanisms will use provided permissions. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

__Table 2\. Navigation__
| [← Previous: Remote Component Bootstrapping](remote-component-bootstrapping.html) | [Next: Back to Microfrontend Bootstrapping →](../../../index.html) |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
