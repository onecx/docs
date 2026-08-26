# @onecx/react-integration-interface

## [](#overview)Overview

`@onecx/react-integration-interface` library is a set of tools aiming to ease the development of React applications integrated with OneCX by utilizing and extending functionalities of [@onecx/integration-interface](../../../onecx-portal-ui-libs/libraries/integration-interface.html). This library offers contexts containing a set of functionalities useful for integrating Microfrontends with OneCX without directly utilizing Topics.

## [](#contexts)Contexts

### [](#app-state-provider)App State Provider

Usage

**Access information about the platform state**.

This context creates new instances of several Topics that contain information about the current state of the platform and makes sure they are cleaned up correctly on destruction.

Example

**Wrap your app with the provider and read topics with `useAppState`.**

```tsx
import { AppStateProvider, useAppState } from "@onecx/react-integration-interface";

const Status = () => {
  const { currentWorkspace$ } = useAppState();
  // currentWorkspace$.subscribe((ws) => console.log(ws));
  return null;
};

export const App = () => (
  <AppStateProvider>
    <Status />
  </AppStateProvider>
);
```

Topics used

* [GlobalErrorTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#global-error-topic)
* [GlobalLoadingTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#global-loading-topic)
* [CurrentMfeTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-mfe-topic)
* [CurrentLocationTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-location-topic)
* [CurrentPageTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-page-topic)
* [CurrentWorkspaceTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-workspace-topic)
* [IsAuthenticatedTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#is-authenticated-topic)

Dependencies

None

API

**App State Provider** properties enable access to topic instances:

__Table 1\. App State Provider properties__
| Property name     | Type                                                                                                                | Description                                                                                                                                                              |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| globalError$      | [GlobalErrorTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#global-error-topic)           | [GlobalErrorTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#global-error-topic) instance.                                                      |
| globalLoading$    | [GlobalLoadingTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#global-loading-topic)       | [GlobalLoadingTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#global-loading-topic) instance.                                                  |
| currentMfe$       | [CurrentMfeTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-mfe-topic)             | [CurrentMfeTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-mfe-topic) instance.                                                        |
| currentLocation$  | [CurrentLocationTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-location-topic)   | [CurrentLocationTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-location-topic) instance.                                              |
| currentPage$      | [CurrentPageTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-page-topic)           | [CurrentPageTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-page-topic) instance. Emits only when page path matches document location. |
| currentWorkspace$ | [CurrentWorkspaceTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-workspace-topic) | [CurrentWorkspaceTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-workspace-topic) instance.                                            |
| isAuthenticated$  | [IsAuthenticatedTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#is-authenticated-topic)   | [IsAuthenticatedTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#is-authenticated-topic) instance.                                              |
| currentPortal$    | [CurrentWorkspaceTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-workspace-topic) | Deprecated. Use currentWorkspace$ instead.                                                                                                                               |

### [](#configuration-provider)Configuration Provider

Usage

**Initialize and access configuration variables for a platform**.

This provider loads configuration variables for the application and exposes them via the ConfigurationTopic.

Example

**Provide defaults and read configuration via `useConfiguration`.**

```tsx
import {
  ConfigurationProvider,
  useConfiguration,
} from "@onecx/react-integration-interface";

const ConfigInfo = () => {
  const { config } = useConfiguration();
  return <pre>{JSON.stringify(config, null, 2)}</pre>;
};

export const App = () => (
  <ConfigurationProvider defaultConfig={{ appId: "my-app", portalId: "portal" }}>
    <ConfigInfo />
  </ConfigurationProvider>
);
```

Topics used

* [ConfigurationTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#configuration-topic)

Dependencies

* HttpClient

API

**Configuration Provider** properties:

__Table 2\. Configuration Provider properties__
| Property name | Type                                                                                                         | Description                                                                                                            |
| ------------- | ------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| config$       | [ConfigurationTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#configuration-topic) | [ConfigurationTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#configuration-topic) instance. |
| isInitialized | Promise<void>                                                                                                | Promise resolved when Configuration Provider is initialized.                                                           |
| config        | Config \| null                                                                                               | Current config snapshot.                                                                                               |

**Configuration Provider** methods can be used for platform configuration variable management:

__Table 3\. Configuration Provider methods__
| Method signature                           | Return type                                                                                                      | Description                                                                                                     |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| init()                                     | Promise<boolean>                                                                                                 | Initializes Configuration Service by loading configuration variables and publishes them via ConfigurationTopic. |
| getProperty(key: CONFIG\_KEY)              | Promise<string \| undefined>                                                                                     | Gets value set for a key from topic.                                                                            |
| async setProperty(key: string, val:string) | Promise<void>                                                                                                    | Updates the value for a key in the configuration. Publishes new message via ConfigurationTopic.                 |
| getConfig()                                | Promise<[Config](../../../onecx-portal-ui-libs/libraries/integration-interface.html#config-object) \| undefined> | Gets all configuration variables defined for the app from the topic.                                            |

### [](#theme-provider)Theme Provider

Usage

**Change the page display style by applying Themes**.

This provider exposes the current theme topic and keeps its lifecycle scoped to the React tree.

Example

**Wrap the tree and read the current theme topic.**

```tsx
import { ThemeProvider, useTheme } from "@onecx/react-integration-interface";

const ThemeStatus = () => {
  const { currentTheme$ } = useTheme();
  // currentTheme$.subscribe((theme) => console.log(theme));
  return null;
};

export const App = () => (
  <ThemeProvider>
    <ThemeStatus />
  </ThemeProvider>
);
```

Topics used

* [CurrentThemeTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-theme-topic)

API

**Theme Provider** properties enable access to topic instances:

__Table 4\. Theme Provider properties__
| Property name | Type                                                                                                        | Description                                                                                                           |
| ------------- | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| currentTheme$ | [CurrentThemeTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-theme-topic) | [CurrentThemeTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#current-theme-topic) instance. |

\=== User Provider

Usage

**Access the user’s data, settings and permissions**.

This service contains user-related information and allows checking user permissions by utilizing Topics.

Example

**Provide user context and check permissions.**

```tsx
import { UserProvider, useUserService } from "@onecx/react-integration-interface";

const Permissions = () => {
  const { hasPermission } = useUserService();
  // hasPermission("MY_PERMISSION").then(console.log);
  return null;
};

export const App = () => (
  <UserProvider>
    <Permissions />
  </UserProvider>
);
```

Topics used

* [UserProfileTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#user-profile-topic)
* [PermissionsTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#permissions-topic)

API

**User Provider** properties enable access to the user’s information:

__Table 5\. User Provider properties__
| Property          | Type                                                                                                      | Description                                                                                                                                                                                                                   |
| ----------------- | --------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| profile$          | [UserProfileTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#user-profile-topic) | [UserProfileTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#user-profile-topic) instance.                                                                                                           |
| lang$             | BehaviorSubject<string>                                                                                   | User’s language. For every new message in the [UserProfileTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#user-profile-topic), the language will be updated based on the user’s locale information. |
| isInitialized     | Promise<void>                                                                                             | Promise resolved when User Service is initialized.                                                                                                                                                                            |
| permissionsTopic$ | [PermissionsTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#permissions-topic)  | [PermissionsTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#permissions-topic) instance.                                                                                                            |

**User Provider** methods:

__Table 6\. User Provider methods__
| Method Signature                                   | Return Type            | Description                                                                               |
| -------------------------------------------------- | ---------------------- | ----------------------------------------------------------------------------------------- |
| getPermissions()                                   | Observable<string\[\]> | Returns the permissions stream from PermissionsTopic.                                     |
| hasPermission(permissionKey: string \| string\[\]) | Promise<boolean>       | Checks if user has specified permission/permissions using PermissionTopic’s latest value. |

### [](#parameters-provider)Parameters Provider

Usage

**Access application parameters published by the shell.**

Topics used

* [ParametersTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#parameters-topic)

Example

**Read a parameter inside the provider.**

```tsx
import { ParametersProvider, useParameters } from "@onecx/react-integration-interface";

const Params = () => {
  const { get } = useParameters();
  // get("feature.flag", false).then(console.log);
  return null;
};

export const App = () => (
  <ParametersProvider>
    <Params />
  </ParametersProvider>
);
```

API

**Parameters Provider** properties:

__Table 7\. Parameters Provider properties__
| Property name | Type                                                                                                   | Description                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| parameters$   | [ParametersTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#parameters-topic) | [ParametersTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#parameters-topic) instance. |

**Parameters Provider** methods:

__Table 8\. Parameters Provider methods__
| Method signature                                                        | Return type | Description                                                             |
| ----------------------------------------------------------------------- | ----------- | ----------------------------------------------------------------------- |
| get(key: string, defaultValue: T, productName?: string, appId?: string) | Promise<T>  | Resolves a parameter value for the current MFE (falls back to default). |

### [](#portal-message-provider)Portal Message Provider

Usage

**Publish translated toast messages through the shell.**

Topics used

* [MessageTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#message-topic)

Example

**Publish a success message from a component.**

```tsx
import {
  PortalMessageProvider,
  usePortalMessage,
} from "@onecx/react-integration-interface";

const Notify = () => {
  const { success } = usePortalMessage();
  // success({ summaryKey: "saved", detailKey: "saved.detail" });
  return null;
};

export const App = () => (
  <PortalMessageProvider>
    <Notify />
  </PortalMessageProvider>
);
```

API

**Portal Message Provider** methods:

__Table 9\. Portal Message Provider methods__
| Method signature                                     | Return type   | Description                                              |
| ---------------------------------------------------- | ------------- | -------------------------------------------------------- |
| success(msg) / info(msg) / warning(msg) / error(msg) | Promise<void> | Publishes a message with translated summary/detail keys. |

### [](#remote-components-provider)Remote Components Provider

Usage

**Access the list of remote components published by the shell.**

Topics used

* [RemoteComponentsTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#remote-components-topic)

Example

**Read remote components from the context.**

```tsx
import {
  RemoteComponentsProvider,
  useRemoteComponents,
} from "@onecx/react-integration-interface";

const Remotes = () => {
  const { remoteComponents$ } = useRemoteComponents();
  // remoteComponents$.subscribe((list) => console.log(list));
  return null;
};

export const App = () => (
  <RemoteComponentsProvider>
    <Remotes />
  </RemoteComponentsProvider>
);
```

API

**Remote Components Provider** properties:

__Table 10\. Remote Components Provider properties__
| Property name     | Type                                                                                                                | Description                                                                                                                   |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| remoteComponents$ | [RemoteComponentsTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#remote-components-topic) | [RemoteComponentsTopic](../../../onecx-portal-ui-libs/libraries/integration-interface.html#remote-components-topic) instance. |

### [](#shell-capability)Shell Capability

Usage

**Check shell capabilities before using optional topics.**

Example

**Set and check capabilities once during bootstrapping.**

```ts
import { setCapabilities, hasCapability } from "@onecx/react-integration-interface";

setCapabilities(["PORTAL_SEARCH"]);
const canSearch = hasCapability("PORTAL_SEARCH");
```

API

**Shell capability** methods:

__Table 11\. Shell capability methods__
| Method signature                              | Return type | Description                                        |
| --------------------------------------------- | ----------- | -------------------------------------------------- |
| setCapabilities(capabilities: Capability\[\]) | void        | Sets the list of shell capabilities on globalThis. |
| hasCapability(capability: Capability)         | boolean     | Checks if a capability is present.                 |

### [](#image-repository-provider)Image Repository Provider

Usage

**Expose an image repository service from the integration interface.**

Note

The current implementation is commented out in the library source and not active. This section documents the intended API if it is re-enabled.

Example

**Provide the image repository service (when enabled).**

```tsx
import {
  ImageRepositoryProvider,
  useImageRepository,
} from "@onecx/react-integration-interface";

const Images = () => {
  const { imageRepositoryService } = useImageRepository();
  // imageRepositoryService.getImage("logo");
  return null;
};

export const App = () => (
  <ImageRepositoryProvider>
    <Images />
  </ImageRepositoryProvider>
);
```

API

**Image Repository Provider** properties:

__Table 12\. Image Repository Provider properties__
| Property name          | Type                                                                                                                  | Description                        |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| imageRepositoryService | [ImageRepositoryService](../../../onecx-portal-ui-libs/libraries/integration-interface.html#image-repository-service) | Image repository service instance. |

### [](#workspace-hook)Workspace Hook

Usage

**Manage Workspace resources**.

This hook offers set of methods useful when developing Microfrontends referencing other Applications via routing.

Example

**Wrap your app with the required providers and use the hook in a component.**

```tsx
import {
  AppStateProvider,
  useWorkspace,
} from "@onecx/react-integration-interface";

const WorkspaceLinks = () => {
  const { getUrl } = useWorkspace();

  // Example: subscribe to the Observable to get the URL
  // getUrl("product", "app").subscribe((url) => console.log(url));

  return null;
};

export const App = () => (
  <AppStateProvider>
    <WorkspaceLinks />
  </AppStateProvider>
);
```

Topics used

None.

Dependencies

* HttpClient
* [AppStateProvider](#app-state-provider)

react-utils

* [@onecx/react-utils](react-utils.html)includes `withApp`, which wraps your component with the base providers and styling helpers (globals, PrimeReact isolation, app styles, base providers). Use it to bootstrap an application with the expected OneCX context.

API

**Workspace Hook** \- **useWorkspace** can be used for constructing routes to Applications:

__Table 13\. Workspace Hook methods__
| Method signature                                                                                               | Return type         | Description                                                                                                                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| getUrl(productName: string, appId: string, endpointName?: string, endpointParameters?:Record<string, unknown>) | Observable<string>  | Constructs a valid url for a desired Application in context of the current Workspace. It is possible to use [Route](../../../onecx-portal-ui-libs/libraries/integration-interface.html#Route-object) endpoints to further customize an accessed resource.       |
| doesUrlExistFor(productName: string, appId: string, endpointName?: string)                                     | Observable<boolean> | Checks if a valid url exists for a desired Application in context of the current Workspace. It is possible to use [Route](../../../onecx-portal-ui-libs/libraries/integration-interface.html#Route-object) endpoints to further customize an accessed resource. |
