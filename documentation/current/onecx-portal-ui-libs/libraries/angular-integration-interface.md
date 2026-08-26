# Library: @onecx/angular-integration-interface

## [](#overview)Overview

`@onecx/angular-integration-interface` library is a set of tools aiming to ease the development of Angular applications integrated with OneCX by utilizing and extending functionalities of [@onecx/integration-interface](integration-interface.html). This library offers Injectable services exposing a set of functionalities useful for integrating Microfrontends with OneCX without directly utilizing Topics.

## [](#injection-tokens)Injection Tokens

### [](#dynamic-container)Dynamic Container

Usage

**Get a reference to the container for dynamic content insertion of the Microfrontend or create one if it doesn’t exist**.

This injection token allows accessing the container element for dynamic content insertion of the Microfrontend. It should be used when creating new elements dynamically and inserting them into the DOM outside of the Angular component tree (e.g. modals, popups appended to the body, etc.). If the container element doesn’t exist, it will be created and appended to the body.

## [](#services)Services

### [](#app-config-service)App Config Service

Usage

**Initialize and access configuration variables for a specific Microfrontend**.

It is similar to [ConfigurationService](#configuration-service), however **App Config Service** should be used for a Microfrontend configuration management. If sharing the configuration variable with multiple Microfrontends is desired, please use [ConfigurationService](#configuration-service) and provide variables via Shell Application.

Topics used

None

Dependencies

* HttpClient

API

**App Config Service** properties enable access to the config data directly:

__Table 1\. App Config Service properties__
| Property name | Type                                         | Description                                         |
| ------------- | -------------------------------------------- | --------------------------------------------------- |
| config$       | BehaviorSubject<{ \[key: string\]: string }> | BehaviorSubject for Application configuration data. |

**App Config Service** methods can be used for Microfrontend configuration variable management:

__Table 2\. App Config Service methods__
| Method signature                           | Return type                 | Description                                                                                                                                  |
| ------------------------------------------ | --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| init(baseUrl: string)                      | Promise<void>               | Initializes App Config Service by loading configuration variables. The configuration will be loaded from the {baseUrl}/assets/env.json file. |
| getProperty(key: string)                   | string \| undefined         | Gets the value for a key from **config$**.                                                                                                   |
| async setProperty(key: string, val:string) | void                        | Updates the value for a key in **config$**.                                                                                                  |
| getConfig()                                | { \[key: string\]: string } | Gets all configuration variables defined for the Microfrontend.                                                                              |

### [](#app-state-service)App State Service

Usage

**Access information about the platform state**.

This service creates new instances of several Topics that contain information about the current state of the platform and makes sure they are cleaned up correctly on destruction.

Topics used

* [GlobalErrorTopic](integration-interface.html#global-error-topic)
* [GlobalLoadingTopic](integration-interface.html#global-loading-topic)
* [CurrentMfeTopic](integration-interface.html#current-mfe-topic)
* [CurrentPageTopic](integration-interface.html#current-page-topic)
* [CurrentWorkspaceTopic](integration-interface.html#current-workspace-topic)
* [IsAuthenticatedTopic](integration-interface.html#is-authenticated-topic)

Dependencies

None

API

**App State Service** properties enable access to topic instances:

__Table 3\. App State Service properties__
| Property name     | Type                                                                        | Description                                                                           |
| ----------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| globalError$      | [GlobalErrorTopic](integration-interface.html#global-error-topic)           | [GlobalErrorTopic](integration-interface.html#global-error-topic) instance.           |
| globalLoading$    | [GlobalLoadingTopic](integration-interface.html#global-loading-topic)       | [GlobalLoadingTopic](integration-interface.html#global-loading-topic) instance.       |
| currentMfe$       | [CurrentMfeTopic](integration-interface.html#current-mfe-topic)             | [CurrentMfeTopic](integration-interface.html#current-mfe-topic) instance.             |
| currentPage$      | [CurrentPageTopic](integration-interface.html#current-page-topic)           | [CurrentPageTopic](integration-interface.html#current-page-topic) instance.           |
| currentWorkspace$ | [CurrentWorkspaceTopic](integration-interface.html#current-workspace-topic) | [CurrentWorkspaceTopic](integration-interface.html#current-workspace-topic) instance. |
| isAuthenticated$  | [IsAuthenticatedTopic](integration-interface.html#is-authenticated-topic)   | [IsAuthenticatedTopic](integration-interface.html#is-authenticated-topic) instance.   |
| currentPortal$    | [CurrentWorkspaceTopic](integration-interface.html#current-workspace-topic) | Deprecated. Use currentWorkspace$ instead.                                            |

### [](#configuration-service)Configuration Service

Usage

**Initialize and access configuration variables for a platform**.

This service is initialized by, and contains configuration variables, for the Shell Application that could be used in any place on the platform.

[ConfigurationService](#configuration-service) **should not be initialized by Microfrontends**. They can utilize specific functionality of this service to access and update configuration data.

Topics used

* [ConfigurationTopic](integration-interface.html#configuration-topic)

Dependencies

* HttpClient

API

**Configuration Service** properties:

__Table 4\. Configuration Service properties__
| Property name | Type                                                                 | Description                                                                    |
| ------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| config$       | [ConfigurationTopic](integration-interface.html#configuration-topic) | [ConfigurationTopic](integration-interface.html#configuration-topic) instance. |
| isInitialized | Promise<void>                                                        | Promise resolved when Configuration Service is initialized.                    |

**Configuration Service** methods can be used for platform configuration variable management:

__Table 5\. Configuration Service methods__
| Method signature                           | Return type                                        | Description                                                                                                                                                 |
| ------------------------------------------ | -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| init()                                     | Promise<boolean>                                   | Initializes Configuration Service by loading Shell configuration variables and publishes them via ConfigurationTopic. Should not be used in Microfrontends. |
| getProperty(key: CONFIG\_KEY)              | string                                             | Gets value set for a key from topic.                                                                                                                        |
| async setProperty(key: string, val:string) | void                                               | Updates the value for a key in the configuration. Publishes new message via ConfigurationTopic.                                                             |
| getConfig()                                | [Config](integration-interface.html#config-object) | Gets all configuration variables defined for the app from the topic.                                                                                        |

### [](#icon-service)Icon Service

Usage

Request icons by name and receive a CSS class to apply in templates. Offers a Promise-based API to await icon availability, with optional fallback class support.

Topics used

* [IconTopic](integration-interface.html#icon-topic)

Dependencies

None

API

**Icon Service** methods:

__Table 6\. Icon Service methods__
| Method signature                                            | Return type                                 | Description             |                                                                                                                |
| ----------------------------------------------------------- | ------------------------------------------- | ----------------------- | -------------------------------------------------------------------------------------------------------------- |
| requestIcon(name: string, type?: 'svg' \| 'background'      | 'background-before')                        | string                  | Requests an icon and returns the CSS class immediately; triggers loading if needed.                            |
| requestIconAsync(name: string, type?: 'svg' \| 'background' | 'background-before')                        | Promise<string \| null> | Resolves with the CSS class when available, or null when the icon cannot be found and no fallback is provided. |
| requestIconAsync(name: string, type: 'svg' \| 'background'  | 'background-before', fallbackClass: string) | Promise<string>         | Resolves with the CSS class when available, or fallbackClass when the icon cannot be found.                    |

| |  See [IconService](../service/icon-service.html) for examples, rendering styles, and cache semantics. |
| ------------------------------------------------------------------------------------------------------- |

### [](#portal-message-service)Portal Message Service

Usage

**Display messages for a short period in an overlay on the top of the page**.

This service is a wrapper for [MessageTopic](integration-interface.html#message-topic) that should be used to display messages using translation keys.

Topics used

* [MessageTopic](integration-interface.html#message-topic)

Dependencies

* TranslateService

API

**Portal Message Service** properties enable access to the topic instances:

__Table 7\. Portal Message Service properties__
| Property name | Type                                                     | Description                                                        |
| ------------- | -------------------------------------------------------- | ------------------------------------------------------------------ |
| message$      | [MessageTopic](integration-interface.html#message-topic) | [MessageTopic](integration-interface.html#message-topic) instance. |

**Portal Message Service** methods can be used for displaying various messages:

__Table 8\. Portal Message Service methods__
| Method signature                         | Return type | Description                                                                                                                  |
| ---------------------------------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------- |
| success(msg: [Message](#Message-object)) | void        | Display message with 'success' severity. Publishes new message via [MessageTopic](integration-interface.html#message-topic). |
| info(msg: [Message](#Message-object))    | void        | Display message with 'info' severity. Publishes new message via [MessageTopic](integration-interface.html#message-topic).    |
| error(msg: [Message](#Message-object))   | void        | Display message with 'error' severity. Publishes new message via [MessageTopic](integration-interface.html#message-topic).   |
| warning(msg: [Message](#Message-object)) | void        | Display message with 'warning' severity. Publishes new message via [MessageTopic](integration-interface.html#message-topic). |

**Message object** accepted by the **Portal Message Service** methods extends the **Message object** used by the [MessageTopic](integration-interface.html#message-topic) with the following properties:

__Table 9\. Message object extensions__
| Property name      | Type   | Description                                         |
| ------------------ | ------ | --------------------------------------------------- |
| summaryKey?        | string | Translation key of the Message summary text.        |
| summaryParameters? | object | Translation parameters of the Message summary text. |
| detailKey?         | string | Translation key of the Message detail text.         |
| detailParameters?  | object | Translation parameters of the Message detail text.  |

### [](#remote-components-service)Remote Components Service

Usage

**Access Remote Components' information**.

This service creates a new instance of [RemoteComponentsTopic](integration-interface.html#remote-components-topic) which contains information about the Remote Components and makes sure it is cleaned up correctly on destroy.

Topics used

* [RemoteComponentsTopic](integration-interface.html#remote-components-topic)

API

**Remote Components Service** properties enable access to topic instances:

__Table 10\. Remote Components Service properties__
| Property name     | Type                                                                        | Description                                                                           |
| ----------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| remoteComponents$ | [RemoteComponentsTopic](integration-interface.html#remote-components-topic) | [RemoteComponentsTopic](integration-interface.html#remote-components-topic) instance. |

### [](#theme-service)Theme Service

Usage

**Change the page display style by applying Themes**.

This service allows changing the currently used Theme by applying it to the document and informs about it via a new message in the [CurrentThemeTopic](integration-interface.html#current-theme-topic).

Topics used

* [CurrentThemeTopic](integration-interface.html#current-theme-topic)

Dependencies

* HttpClient
* [ConfigurationService](#configuration-service)

API

**Theme Service** properties enable access to topic instances:

__Table 11\. Theme Service properties__
| Property name | Type                                                                | Description                                                                   |
| ------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| currentTheme$ | [CurrentThemeTopic](integration-interface.html#current-theme-topic) | [CurrentThemeTopic](integration-interface.html#current-theme-topic) instance. |
| baseUrlV1     | string                                                              | Deprecated.                                                                   |

**Theme Service** methods:

__Table 12\. Theme Service methods__
| Method signature                                               | Return type   | Description                                                                                                                                                                                                                   |
| -------------------------------------------------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| apply(theme: [Theme](integration-interface.html#theme-object)) | Promise<void> | Applies [Theme](integration-interface.html#theme-object) via document style manipulation (styles will be lost on page exit). Publishes a new message via [CurrentThemeTopic](integration-interface.html#current-theme-topic). |
| getThemeHref(themeId: string)                                  | string        | Deprecated.                                                                                                                                                                                                                   |
| loadAndApplyTheme(themeName: string)                           | void          | Deprecated.                                                                                                                                                                                                                   |

### [](#user-service)User Service

Usage

**Access the user’s data, settings and permissions**.

This service contains user-related information and allows checking user permissions by utilizing Topics.

Topics used

* [UserProfileTopic](integration-interface.html#user-profile-topic)
* [PermissionsTopic](integration-interface.html#permissions-topic)

API

**User Service** properties enable access to the user’s information:

__Table 13\. User Service properties__
| Property name    | Type                                                              | Description                                                                                                                                                                           |
| ---------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| profile$         | [UserProfileTopic](integration-interface.html#user-profile-topic) | [UserProfileTopic](integration-interface.html#user-profile-topic) instance.                                                                                                           |
| lang$            | BehaviorSubject<string>                                           | User’s language. For every new message in the [UserProfileTopic](integration-interface.html#user-profile-topic), the language will be updated based on the user’s locale information. |
| isInitialized    | Promise<void>                                                     | Promise resolved when User Service is initialized.                                                                                                                                    |
| getPermissions() | Observable<string\[\]>                                            | Observable with list of permissions for the current user.                                                                                                                             |
| permissions$     | BehaviorSubject<string\[\]>                                       | Deprecated.                                                                                                                                                                           |

**User Service** methods:

__Table 14\. User Service methods__
| Method signature                      | Return type   | Description |
| ------------------------------------- | ------------- | ----------- |
| \`hasPermission(permissionKey: string | string\[\])\` | boolean     |

### [](#workspace-service)Workspace Service

Usage

**Manage Workspace resources**.

This service offers set of methods useful when developing Microfrontends referencing other Applications via routing.

Topics used

None.

Dependencies

* HttpClient
* [AppStateService](#app-state-service)

API

**Workspace Service** methods can be used for constructing routes to Applications:

__Table 15\. Workspace Service methods__
| Method signature                                                                                               | Return type         | Description                                                                                                                                                                                                             |
| -------------------------------------------------------------------------------------------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| getUrl(productName: string, appId: string, endpointName?: string, endpointParameters?:Record<string, unknown>) | Observable<string>  | Constructs a valid url for a desired Application in context of the current Workspace. It is possible to use [Route](integration-interface.html#Route-object) endpoints to further customize an accessed resource.       |
| doesUrlExistFor(productName: string, appId: string, endpointName?: string)                                     | Observable<boolean> | Checks if a valid url exists for a desired Application in context of the current Workspace. It is possible to use [Route](integration-interface.html#Route-object) endpoints to further customize an accessed resource. |
