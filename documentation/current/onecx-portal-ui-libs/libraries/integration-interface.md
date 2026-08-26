# Library: @onecx/integration-interface

## [](#overview)Overview

`@onecx/integration-interface` library is a set of tools written in **Typescript** that enables communication between Microfrontends. The library can be used in any desired technology.

| |  For Angular-based applications, the [@onecx/angular-integration-interface](angular-integration-interface.html) library is available. It is a set of tools aiming to ease the development of Angular applications integrated with OneCX. For more information, please refer [here](angular-integration-interface.html). |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#topics)Topics

A Topic is a similar concept to an Observable. They operate on messages passed between UI Apps using browser memory. Each topic:

* has unique name
* has version
* can publish new message
* can be subscribed to and piped for handling new messages
* can be destroyed to prevent listening to new messages With multiple UI Apps having the same Topic instantiated (with the same name), they can communicate with each other based on the publisher-subscriber model. Whenever any Topic instance publishes new message, subscribers for all instances will read the message eventually allowing them to react on new information.

### [](#configuration-topic)Configuration Topic

Usage

Read information about the **platform configuration**.

Shell actions

The Shell loads configuration variables and publishes them to the Topic as the first message.

Data

**Config object** with string entries, where each entry represents a configuration variable:

```typescript
interface Config { [key: string]: string }
```

| |  For Angular-based applications, the [@onecx/angular-integration-interface offers an Injectable ConfigurationService service](angular-integration-interface.html#configuration-service) exposing functions useful when dealing with configuration management. This service is used by the Shell Application. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#current-mfe-topic)Current Mfe Topic

Usage

Read information about the **currently accessed Microfrontend**. The only publisher for this Topic should be the host Application (Shell).

Shell actions

On Route activation publishes information about accessed MFE.

Data

**MfeInfo object** describing currently accessed Microfrontend with the following structure:

__Table 1\. MfeInfo structure__
| Property name | Type   | Description                                                                                                                |
| ------------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| appId         | string | Unique identifier of the Microfrontend.                                                                                    |
| baseHref      | string | Microfrontend’s base path within the current Workspace, i.e. '/workspace/mfe\_base\_path'.                                 |
| mountPath     | string | Microfrontend’s mount path containing Workspace and application base path, i.e. '/workspace/mfe\_base\_path'.              |
| productName   | string | Name of the Application currently accessed Microfrontend is part of.                                                       |
| remoteBaseUrl | string | Microfrontend’s remote URL to be used when accessing its content (remote entry file, assets, etc.), e.g. '/mfe/mfe\_name'. |
| shellName     | string | Name of the currently used shell, always 'portal'.                                                                         |
| displayName?  | string | Name for Microfrontend to display.                                                                                         |
| elementName?  | string | Name of the HTML element, Microfrontend’s module should be displayed in, e.g. 'mfe-component'.                             |
| remoteName?   | string | Name of the remote set up in Microfrontend’s webpack (Used for WebComponents integration within platform).                 |
| version?      | string | Version of the Microfrontend.                                                                                              |
| remote?       | string | Deprecated.                                                                                                                |

| |  For Angular based applications [@onecx/angular-integration-interface offers an Injectable AppStateService service](angular-integration-interface.html#app-state-service) exposing functions usefull when dealing with application state management. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### [](#current-page-topic)Current Page Topic

Usage

Read information about the **currently accessed Page**. The only publisher for this Topic should be **PortalPageComponent(ocx-portal-page)**.

Shell actions

None

Important actions

When creating Microfrontend’s content, use **PortalPageComponent(ocx-portal-page)**. On its initialization, a new PageInfo message will be published based on data provided to the component via Inputs.

Data

**PageInfo object** describing currently accessed Page with the following structure:

__Table 2\. PageInfo structure__
| Property name  | Type   | Description                                                                                                                                                          |
| -------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| path           | string | Complete path of the current Page containing Shell deployment path, Workspace base path and Microfrontend’s accessed path, e.g. '/shell/workspace/mfe/details/id-1'. |
| helpArticleId? | string | ID of help article associated with the Page.                                                                                                                         |
| pageName?      | string | Unique name of the Page.                                                                                                                                             |
| permission?    | string | Permission required to access Page content.                                                                                                                          |
| applicationId? | string | Deprecated.                                                                                                                                                          |

| |  For Angular based applications [@onecx/angular-integration-interface offers an Injectable AppStateService service](angular-integration-interface.html#app-state-service) exposing functions usefull when dealing with application state management. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### [](#current-theme-topic)Current Theme Topic

Usage

Read information about the **currently applied Theme**. Writing new messages to this Topic will not change the current Theme applied to a page, which might cause inconsistency. If it is desired to change the current Theme, please consider using [Theme Service](angular-integration-interface.html#theme-service). For other technologies, make sure to apply the chosen Theme before publishing a new message to the Topic.

Shell actions

During Workspace construction, Shell is going to load and apply Theme assigned to the Workspace. That Theme’s information will also be published to the Topic.

Data

**Theme object** describing currently applied Theme with the following structure:

__Table 3\. Theme structure__
| Property name     | Type                                             | Description                                                                                                                                                                                                                                                                                                             |
| ----------------- | ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| description?      | string                                           | Description of the Theme.                                                                                                                                                                                                                                                                                               |
| faviconUrl?       | string                                           | ?                                                                                                                                                                                                                                                                                                                       |
| id?               | string                                           | Unique identifier of the Theme.                                                                                                                                                                                                                                                                                         |
| logoUrl?          | string                                           | URL to an external image to be used as Theme logo.                                                                                                                                                                                                                                                                      |
| name?             | string                                           | Name of the Theme                                                                                                                                                                                                                                                                                                       |
| properties?       | { \[key: string\]: { \[key: string\]: string } } | Object containing CSS variables used for currently applied theme. It contains an entry for each section in the Theme designer (Font, General, Topbar, Sidebar), where key is the section name and value is an object containing key value pairs representing a certain CSS variable value to be used for a given Theme. |
| assetsUpdateDate? | string                                           | Deprecated.                                                                                                                                                                                                                                                                                                             |
| assetsUrl?        | string                                           | Deprecated.                                                                                                                                                                                                                                                                                                             |
| cssFile?          | string                                           | Deprecated.                                                                                                                                                                                                                                                                                                             |
| previewImageUrl?  | string                                           | Deprecated.                                                                                                                                                                                                                                                                                                             |

| |  For Angular-based applications, the [@onecx/angular-integration-interface offers an Injectable ThemeService service](angular-integration-interface.html#theme-service) exposing functions useful when dealing with theme management. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#current-workspace-topic)Current Workspace Topic

Usage

Read information about the **currently accessed Workspace**. The only publisher for this Topic should be host Application (Shell).

Shell actions

During Workspace construction, Shell is going to publish its information to the Topic.

Data

**Workspace object** describing currently accessed Workspace with the following structure:

__Table 4\. Workspace structure__
| Property name              | Type                           | Description                                           |
| -------------------------- | ------------------------------ | ----------------------------------------------------- |
| baseUrl                    | string                         | Base URL of the Workspace, e.g. '/admin'.             |
| workspaceName              | string                         | Name of the Workspace used as reference.              |
| displayName?               | string                         | Name of the Workspace used for display.               |
| homePage?                  | string                         | Home page URL relative to Workspace, e.g. '/welcome'. |
| routes?                    | Array<[Route](#Route-object)\> | List of routes to Microfrontends for a Workspace.     |
| companyName?               | string                         | Deprecated.                                           |
| footerLabel?               | string                         | Deprecated.                                           |
| id?                        | string                         | Deprecated.                                           |
| logoUrl?                   | string                         | Deprecated.                                           |
| logoSmallImageUrl?         | string                         | Deprecated.                                           |
| portalRoles?               | string\[\]                     | Deprecated.                                           |
| themeId?                   | string                         | Deprecated.                                           |
| themeName?                 | string                         | Deprecated.                                           |
| portalName                 | string                         | Deprecated.                                           |
| description                | string                         | Deprecated.                                           |
| imageUrls                  | string\[\]                     | Deprecated.                                           |
| address                    | object                         | Deprecated.                                           |
| phoneNumber                | string                         | Deprecated.                                           |
| rssFeedUrl                 | string                         | Deprecated.                                           |
| subjectLinks               | object\[\]                     | Deprecated.                                           |
| microfrontendRegistrations | object\[\]                     | Deprecated.                                           |
| userUploaded               | boolean                        | Deprecated.                                           |

**Workspace object** contains a list of routes for registered Microfrontends. Each **Route** has the following structure:

__Table 5\. Route structure__
| Property name  | Type                              | Description                                                                                                                                                                                           |                                                   |
| -------------- | --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| appId          | string                            | Unique identifier of the Microfrontend.                                                                                                                                                               |                                                   |
| baseUrl        | string                            | Microfrontend’s base path within the current workspace, i.e. '/workspace/mfe\_base\_path'.                                                                                                            |                                                   |
| displayName    | string                            | Name for Microfrontend to display.                                                                                                                                                                    |                                                   |
| elementName    | string                            | Name of the HTML element Microfrontend’s module should be displayed in, e.g. 'mfe-component'                                                                                                          |                                                   |
| endpoints      | Array<Endpoint>                   | Array of endpoints to be used by a Microfrontend to navigate to other MFEs safely. Each endpoint contains a name (string) and a path (string) that can be used when deciding on the URL of the pages. |                                                   |
| exposedModule  | string                            | Name of the exposed module to be loaded for a Microfrontend, e.g. './MfeModule'                                                                                                                       |                                                   |
| pathMatch      | 'full' \| 'prefix'                | Path matching strategy of a Route.                                                                                                                                                                    |                                                   |
| productName    | string                            | Name of the Application currently accessed Microfrontend is part of.                                                                                                                                  |                                                   |
| remoteEntryUrl | string                            | URL of the Microfrontend’s remote entry file, e.g. 'mfe/mfe\_base\_path/remoteEntry.js'.                                                                                                              |                                                   |
| remoteName     | string                            | Name of the remote set up in Microfrontend’s webpack (Used for WebComponents integration within platform).                                                                                            |                                                   |
| technology     | 'Angular' \| 'WebComponentScript' | 'WebComponentModule'                                                                                                                                                                                  | Technology used to expose Microfrontend’s module. |
| url            | string                            | Microfrontend’s remote URL to be used when accessing its content (remote entry file, assets, etc.), e.g. '/mfe/mfe\_name'.                                                                            |                                                   |

| |  For Angular based applications [@onecx/angular-integration-interface offers an Injectable AppStateService service](angular-integration-interface.html#app-state-service) exposing functions usefull when dealing with application state management. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### [](#events-topic)Events Topic

Usage

Write and read information about the **custom events within the platform**. Useful whenever it is desired to exchange information between Apps and no Topic has been created for that purpose.

Shell actions

Shell is using EventsTopic to sync its router with navigation events happening in Microfrontend’s routers ([side effect of using webcomponent loading mechanism](../../onecx-docs-overview/module-federation/webcomponents.html#angular%5Fissues)). The following event is used to exchange all navigation events within the OneCX platform:

```typescript
type NavigatedEvent = {
    type: 'navigated';
    payload: NavigatedEventPayload;
};
type NavigatedEventPayload = {
    url: string | undefined;
    isFirst: boolean;
};
```

Data

**Object** containing a type (to distinguish messages) and payload:

```typescript
type TopicEvent Type = { type: string; payload?: unknown | undefined }
```

### [](#global-error-topic)Global Error Topic

Usage

Write and read information about the **global errors within the platform**.

Shell actions

Shell will display the errors published to this Topic in a designated place, regardless of the Microfrontend loaded.

Data

**String** containing information about the global error raised within the platform.

| |  For Angular based applications [@onecx/angular-integration-interface offers an Injectable AppStateService service](angular-integration-interface.html#app-state-service) exposing functions usefull when dealing with application state management. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### [](#global-loading-topic)Global Loading Topic

Usage

Write and read information about the **global loading happening within the platform**.

Shell actions

Shell sets the global loading indicator for the remote content loading period.

Data

**Boolean** indicating whether global loading is happening or not.

| |  For Angular based applications [@onecx/angular-integration-interface offers an Injectable AppStateService service](angular-integration-interface.html#app-state-service) exposing functions usefull when dealing with application state management. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### [](#icon-topic)Icon Topic

Usage

Coordinate icon requests and availability across the platform. Microfrontends publish requests; the Shell loads missing icons and signals completion.

Shell actions

Listens for `IconRequested`, batches missing icon loads, injects CSS for requested render styles, then publishes `IconsReceived`.

Data

**Icon messages and cache** used by the topic and helper utilities:

__Table 6\. Icon-related types__
| Name          | Type                                                                    | Description                                                |                                      |
| ------------- | ----------------------------------------------------------------------- | ---------------------------------------------------------- | ------------------------------------ |
| IconRequested | { type: 'IconRequested'; name: string; classType: 'svg' \| 'background' | 'background-before' }                                      | Published when an icon is requested. |
| IconsReceived | { type: 'IconsReceived' }                                               | Published when the Shell finished loading/injecting icons. |                                      |
| IconCache     | { name: string; type: string; body: string; parent?: string \| null }   | SVG data and metadata for a resolved icon.                 |                                      |

__Table 7\. Global cache__
| window.onecxIcons | Record<string, IconCache \| null | undefined> where undefined means requested but not yet loaded, null means not found, and IconCache means available. |
| ----------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------- |

| |  For Angular applications, see the [Icon Service](../service/icon-service.html) which wraps this topic and utilities. |
| ----------------------------------------------------------------------------------------------------------------------- |

### [](#is-authenticated-topic)Is Authenticated Topic

Usage

Wait for an **authentication indicator**, do certain actions. Whenever this topic is initialized, Microfrontend’s content can assume that the user accessing the page is authenticated.

Shell actions

Shell uses AuthService from the `@onecx/angular-auth` library for authentication. During Shell initialization (via APP\_INITIALIZER), AuthService is initialized. On successful initialization, the message is published to the Topic.

Data

**Empty**

| |  For Angular based applications [@onecx/angular-integration-interface offers an Injectable AppStateService service](angular-integration-interface.html#app-state-service) exposing functions usefull when dealing with application state management. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### [](#message-topic)Message Topic

Usage

Write **messages to be displayed in an overlay on the top of the page**. Useful when it is desired to inform about a certain event happening via a message displayed for a short period of time. Publish a new message to display it.

Shell actions

Shell will listen to messages published via this Topic and will display the message in a designated place.

Data

**Message object** describing message to be displayed with the following structure:

| |  **Message object** structure is based on the [PrimeNG Toast API](https://primeng.org/toast), which is used internally to display messages. |
| --------------------------------------------------------------------------------------------------------------------------------------------- |

| |  For Angular-based applications, the [@onecx/angular-integration-interface offers an Injectable PortalMessageService service](angular-integration-interface.html#portal-message-service) exposing functions useful when dealing with displaying messages. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#permissions-topic)Permissions Topic

Usage

Read **user’s permissions related to current Microfrontend**. The only publisher for this Topic should be the host Application (Shell).

Shell actions

On Route activation publishes information about permissions related to the accessed MFE.

Data

**Array<string>**, each representing user’s permission.

| |  For Angular-based applications, the [@onecx/angular-integration-interface offers an Injectable UserService service](angular-integration-interface.html#user-service) exposing functions useful when dealing with user related data. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#permissions-rpc-topic)Permissions Rpc Topic

Usage

Read the **user’s permissions related to any Application**. Useful when it is desired to check if permission not related to the the current Microfrontend is met for current User (e.g., used for Remote Components). This topic should be used in a request-response fashion. Request messages should have the `permissions` property undefined and should be made by the Microfrontend containing Applications. Response messages will have the `permissions` property defined (`Array<string>`) and should be made by the Shell Application.

Shell actions

Shell is listening to new messages published in the Topic. Whenever a message with the `permissions` property set to `undefined` is read by the Shell, it fetches permissions for the current user related to the requested Application.

Data

**PermissionsRpc object** includes requested Application information and permissions with the following structure:

__Table 8\. PermissionsRpc structure__
| Property name | Type          | Description                                                                                                 |
| ------------- | ------------- | ----------------------------------------------------------------------------------------------------------- |
| appId         | string        | Unique identifier of the Microfrontend.                                                                     |
| productName   | string        | Name of the Application (Microfrontend is part of).                                                         |
| permissions?  | Array<string> | Permissions for the current user regarding provided Application Data. Data filled by the Shell Application. |

| |  For Angular-based applications, the @onecx/angular-remote-components offers an Injectable PermissionService service exposing functions useful when dealing with permission management for Remote Components. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#remote-components-topic)Remote Components Topic

Usage

Read **currently accessed Workspace Remote Components data**. The only publisher for this Topic should be the host Application (Shell).

Shell actions

During Workspace construction, Shell is going to publish information about available Slots and Components to the Topic in the context of the currently accessed Workspace.

Data

**RemoteComponentsInfo object** describing available Remote Components and Slots with the following structure:

__Table 9\. RemoteComponentsInfo structure__
| Property name | Type                                           | Description                                 |
| ------------- | ---------------------------------------------- | ------------------------------------------- |
| components    | [RemoteComponent](#RemoteComponent-object)\[\] | Registered Remote Components for Workspace. |
| slots         | [Slot](#Slot-object)\[\]                       | Registered Slots for Workspace.             |

**RemoteComponent object** describing Remote Component with the following structure:

__Table 10\. RemoteComponent structure__
| Property name  | Type                              | Description                                                                                                                                 |                                             |
| -------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| name           | string                            | Unique name of a Remote Component.                                                                                                          |                                             |
| baseUrl        | string                            | URL of the Remote Component’s Microfrontend to be used when accessing its content (remote entry file, assets, etc.), e.g. '/mfe/mfe\_name'. |                                             |
| remoteEntryUrl | string                            | URL of the Remote Component’s Microfrontend remote entry file, e.g. 'mfe/mfe\_base\_path/remoteEntry.js'.                                   |                                             |
| appId          | string                            | Unique identifier of the Remote Component’s Microfrontend.                                                                                  |                                             |
| productName    | string                            | Name of the Application currently accessed Remote Component’s Microfrontend is part of.                                                     |                                             |
| exposedModule  | string                            | Name of the exposed Remote Component to be loaded, e.g. './MfeRemoteComponent'.                                                             |                                             |
| remoteName     | string                            | Name of the remote set up in Remote Component’s Microfrontend webpack (Used for WebComponents integration within platform).                 |                                             |
| technology     | 'Angular' \| 'WebComponentScript' | 'WebComponentModule'                                                                                                                        | Technology used to expose Remote Component. |

**Slot** object describing Slot with the following structure:

__Table 11\. Slot structure__
| Property name | Type          | Description                                              |
| ------------- | ------------- | -------------------------------------------------------- |
| name          | string        | Name of the Slot.                                        |
| components    | Array<string> | List of Remote Component names registered for this Slot. |

| |  For Angular-basedAngular-based applications, it’s best to utilize the @onecx/angular-remote-components library offering an Injectable SlotService service and SlotComponent useful for working with Remote Components. Those offerings are based on the Remote Components Topic. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#user-profile-topic)User Profile Topic

Usage

Read **current User information**. The only publisher for this Topic should be the host Application (Shell).

Shell actions

During Workspace construction, Shell is going to load and publish information about the current User to the Topic.

Data

**UserProfile object** describing current User with the following structure:

__Table 12\. UserProfile structure__
| Property name       | Type                                                             | Description                                          |
| ------------------- | ---------------------------------------------------------------- | ---------------------------------------------------- |
| person              | [UserPerson](#UserPerson-object)                                 | User personal information.                           |
| userId              | string                                                           | User ID in OneCX platform.                           |
| accountSettings?    | [UserProfileAccountSettings](#UserProfileAccountSettings-object) | User’s account settings.                             |
| organization?       | string                                                           | Name of the User’s organization.                     |
| tenantId?           | string                                                           | Id of the User’s tenant.                             |
| avatar?             | AvatarInfo                                                       | Deprecated.                                          |
| id?                 | string                                                           | Deprecated. Use userId instead.                      |
| identityProvider?   | string                                                           | Deprecated.                                          |
| identityProviderId? | string                                                           | Deprecated.                                          |
| memberships?        | Array<Membership>                                                | Deprecated.                                          |
| tenantName?         | string                                                           | Deprecated. Use tenantId to determine user’s tenant. |

**UserPerson object** describing current User’s personal info with the following structure:

__Table 13\. UserPerson structure__
| Property name | Type                                           | Description          |
| ------------- | ---------------------------------------------- | -------------------- |
| firstName?    | string                                         | User’s first name.   |
| lastName?     | string                                         | User’s last name.    |
| displayName?  | string                                         | User’s display name. |
| email?        | string                                         | User’s email.        |
| address?      | [UserPersonAddress](#UserPersonAddress-object) | User’s address.      |
| phone?        | [UserPersonPhone](#UserPersonPhone-object)     | User’s phone.        |

**UserPersonAddress object** describing current User’s address info with the following structure:

__Table 14\. UserPersonAddress structure__
| Property name | Type   | Description           |
| ------------- | ------ | --------------------- |
| street?       | string | User’s street name.   |
| streetNo?     | string | User’s street number. |
| city?         | string | User’s city.          |
| postalCode?   | string | User’s postal code.   |
| country?      | string | User’s country.       |

**UserPersonPhone object** describing current User’s phone info with the following structure:

__Table 15\. UserPersonPhone structure__
| Property name | Type                   | Description          |
| ------------- | ---------------------- | -------------------- |
| type?         | 'MOBILE' \| 'LANDLINE' | User’s phone type.   |
| number?       | string                 | User’s phone number. |

**UserProfileAccountSettings object** describing current User’s account settings with the following structure:

__Table 16\. UserProfileAccountSettings structure__
| Property name           | Type                                                                                                         | Description                      |
| ----------------------- | ------------------------------------------------------------------------------------------------------------ | -------------------------------- |
| layoutAndThemeSettings? | [UserProfileAccountSettingsLayoutAndThemeSettings](#UserProfileAccountSettingsLayoutAndThemeSettings-object) | User’s layout and theme settings |
| localeAndTimeSettings?  | [UserProfileAccountSettingsLocaleAndTimeSettings](#UserProfileAccountSettingsLocaleAndTimeSettings-object)   | User’s locale and time settings. |
| notificationSettings?   | [UserProfileAccountSettingsNotificationSettings](#UserProfileAccountSettingsNotificationSettings-object)     | Deprecated.                      |
| privacySettings?        | [UserProfileAccountSettingsPrivacySettings](#UserProfileAccountSettingsPrivacySettings-object)               | Deprecated.                      |

**UserProfileAccountSettingsLayoutAndThemeSettings object** describing current User’s layout and theme settings with the following structure:

__Table 17\. UserProfileAccountSettingsLayoutAndThemeSettings structure__
| Property name | Type                     | Description |                            |            |                         |
| ------------- | ------------------------ | ----------- | -------------------------- | ---------- | ----------------------- |
| menuMode?     | 'HORIZONTAL' \| 'STATIC' | 'OVERLAY'   | 'SLIM'                     | 'SLIMPLUS' | Menu mode set for User. |
| colorScheme?  | 'AUTO' \| 'LIGHT'        | 'DARK'      | Color scheme set for User. |            |                         |

**UserProfileAccountSettingsLocaleAndTimeSettings object** describing current User’s locale and time settings with the following structure:

__Table 18\. UserProfileAccountSettingsLocaleAndTimeSettings structure__
| Property name | Type   | Description      |
| ------------- | ------ | ---------------- |
| locale?       | string | User’s locale.   |
| timezone?     | string | User’s timezone. |

| |  For Angular-based applications, the [@onecx/angular-integration-interface offers an Injectable UserService service](angular-integration-interface.html#user-service) exposing functions useful when dealing with user related data. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
