# Permissions Handling

An Angular application often needs to show, hide, or disable parts of its UI depending on what the current user is allowed to do — for example, rendering an **Edit** button only for users who hold the `USER#EDIT` permission. The [OneCX permission management](../../onecx-permission/index.html) application decides which permissions a user has (derived from their roles); this feature is how an application **reacts** to those permissions by rendering UI conditionally.

For the deep dive on where permissions come from and how they relate to the authentication provider and the user’s session, see [Authentication](../concepts/authentication.html).

| |  Angular applications use the directives and PermissionService described on the subpages below. The React libraries have no \*ocxIfPermission\-equivalent conditional-rendering API, but React applications can read the current user’s permissions with the usePermission hook / PermissionProvider — see [Checking permissions in code (React)](permissions/react/checking-permissions-in-code.html)\[Checking permissions in code (React)\]. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#how-it-works)How it works

In OneCX, permissions are assigned to roles and roles to users, so a given user ends up with a set of permissions that the [OneCX permission management](../../onecx-permission/index.html) application has resolved. The shell exposes the current user’s permissions to integrated applications through the [User Service](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#user-service). From there an application can check permissions directly in code — through the `PermissionService` — or conditionally render template content — through the permission directives, both covered on the subpages below.

The permission strings follow the `<RESOURCE>#<ACTION>` convention (for example, `USER#DELETE`, `ORDER#EXPORT`). What a user is actually permitted to do is configured in the OneCX core applications, not in the application’s own code.

## [](#sub-features)Sub-features

* [Conditional rendering](permissions/angular/conditional-rendering.html)\[Conditional rendering\] — the `*ocxIfPermission` / `*ocxIfNotPermission` directives: rendering or hiding template content based on the current user’s permissions, including `elseTemplate` and `onMissingPermission: 'disable'`.
* [Checking permissions in code (Angular)](permissions/angular/checking-permissions-in-code.html)\[Checking permissions in code (Angular)\] — the `PermissionService.hasPermission()` / `getPermissions()` checks for guards, services, and other logic outside a template, plus how to swap the underlying permission source with a `HAS_PERMISSION_CHECKER`.
* [Checking permissions in code (React)](permissions/react/checking-permissions-in-code.html)\[Checking permissions in code (React)\] — reading the current user’s permissions in a React application with the `usePermission` hook and `PermissionProvider` from `@onecx/react-remote-components`.

## [](#related)Related

* [Authentication](../concepts/authentication.html) — how the shell owns the authentication flow and where a user’s permissions come from.
* [User Service](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#user-service) — the `@onecx/angular-integration-interface` service that resolves the current user’s permissions.
