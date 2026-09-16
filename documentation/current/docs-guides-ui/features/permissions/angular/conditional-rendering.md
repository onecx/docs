# Conditional Rendering

## [](#overview)Overview

Two structural directives render a template based on the current user’s permissions, letting an Angular application conditionally show or hide parts of its UI:

**ocxIfPermission — renders the template only when the user \*has** the required permission(s). **ocxIfNotPermission — renders the template only when the user does \*not** have the required permission(s), which is useful for showing a fallback or hint to users without access. 

Both accept a single permission (a string) or several (an array). When an array is given, all of the listed permissions are required — the check is a logical AND.

| |  The directives resolve the current user’s permissions through the HAS\_PERMISSION\_CHECKER injection token, falling back to the [User Service](../../../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#user-service) when no custom checker is provided. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#ifpermission)`*ocxIfPermission`

Shows the host template only if the user has the required permission(s).

button shown only with the USER#EDIT permission

```html
<button pButton pRipple *ocxIfPermission="'USER#EDIT'">
  {{ 'ACCESS_PAGE_KEY.EDIT' | translate }}
</button>
```

button shown only when every listed permission is present

```html
<button pButton pRipple *ocxIfPermission="['USER#VIEW', 'USER#EXPORT']">
  {{ 'ACCESS_PAGE_KEY.EXPORT' | translate }}
</button>
```

## [](#ifnotpermission)`*ocxIfNotPermission`

Shows the host template only if the user does **not** have the required permission(s). This is useful for displaying fallback UI (a hint or read-only message) to users without access.

fallback hint for users without the USER#VIEW permission

```html
<div class="text-muted" *ocxIfNotPermission="'USER#VIEW'">
  {{ 'ACCESS_PAGE_KEY.NO_ACCESS_HINT' | translate }}
</div>
```

## [](#options)Microsyntax options

Beyond show/hide, both directives support rendering an alternative `elseTemplate` and keeping the UI visible but `disabled` when the permission is missing (`onMissingPermission: 'disable'`). Both directives support the same microsyntax options:

| Option              | Type                | Meaning                                                                                                                              |
| ------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| elseTemplate        | TemplateRef         | Template to render when the permission condition is not met.                                                                         |
| onMissingPermission | 'hide' \| 'disable' | Default is 'hide'. If set to 'disable', the original template is rendered and its root element gets a disabled="disabled" attribute. |
| permissions         | string\[\]          | Optional override list of permissions to use for the check (bypasses the injected checker/service).                                  |

## [](#elsetemplate)`elseTemplate`

Renders an alternative template when the permission condition is not met.

example.html

```html
<button
  pButton
  pRipple
  *ocxIfPermission="'USER#EDIT'; elseTemplate: noEditPermission"
>
  {{ 'ORDER.EDIT' | translate }}
</button>

<ng-template #noEditPermission>
  <p class="text-muted">{{ 'ACCESS_PAGE_KEY.READ_ONLY' | translate }}</p>
</ng-template>
```

For **ocxIfNotPermission, the semantics are inverted: `elseTemplate` is rendered when the user \*does have** the permission(s). 

## [](#onmissingpermission-disable)`onMissingPermission: 'disable'`

Keeping the UI visible but disabled is useful for discoverability — the user can see the control but not interact with it.

example.html

```html
<button
  pButton
  pRipple
  *ocxIfPermission="'USER#DELETE'; onMissingPermission: 'disable'"
>
  {{ 'ORDER.DELETE' | translate }}
</button>
```

| |  The directive adds and removes the disabled attribute on the **root node** of the rendered template. Make sure the template’s root element supports being disabled (e.g. <button>, <input>, some PrimeNG host elements). |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#related)Related

* [Permissions Handling](../../permissions.html)\[Permissions Handling\] — the feature overview, how permissions reach an application, and the `<RESOURCE>#<ACTION>` convention.
* [Checking permissions in code (Angular)](checking-permissions-in-code.html)\[Checking permissions in code (Angular)\] — the `PermissionService` and `HAS_PERMISSION_CHECKER` checks for logic outside a template.
* [User Service](../../../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#user-service) — the `@onecx/angular-integration-interface` service the directives resolve permissions through.
* [Checking permissions in code (React)](../react/checking-permissions-in-code.html)\[Checking permissions in code (React)\] — reading permissions in a React application with `usePermission` / `PermissionProvider`.
