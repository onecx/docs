# Split shell and apps authentication

In OneCX libs v8, auth implementation classes were moved out of `@onecx/angular-auth`. If your app imports auth implementation symbols directly from `@onecx/angular-auth`, your build will fail after upgrading to v8.

This split separates shell-specific authentication logic from regular application token-based authentication.

| |  Shell usage: use @onecx/shell-auth (includes Keycloak-specific logic). Regular OneCX Angular app usage: use only @onecx/angular-auth (token-based authentication). You do not need @onecx/shell-auth or keycloak-js unless you use standalone mode. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

## [](#%5Fwhat%5Fchanged)What changed

The following symbols are no longer exported from `@onecx/angular-auth`:

* `AuthServiceWrapper`
* `provideAuthService`
* `KeycloakAuthService`
* `DisabledAuthService`
* `AuthService`

In v8 these implementation APIs are provided by `@onecx/shell-auth`.

## [](#%5Fonecx%5Fangular%5Fapplications)Onecx Angular applications

1. Use `@onecx/angular-auth` for interceptor/token wiring (`AngularAuthModule` / `provideTokenInterceptor`)
2. Uninstall `keycloak-js` dependency.  
```bash  
npm uninstall keycloak-js  
```

## [](#%5Fonecx%5Fstandalone%5Fapplications%5Fmigration)Onecx Standalone Applications Migration

1. If you use standalone-shell, replace shell auth implementation imports with `@onecx/shell-auth`.
2. Keep `AngularAuthModule` from `@onecx/angular-auth` for regular application interceptor/token wiring.
3. Add `@onecx/shell-auth` with keycloak-js dependency only for standalone-shell authentication.
