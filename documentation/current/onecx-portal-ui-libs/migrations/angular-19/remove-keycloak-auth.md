# Remove @onecx/keycloak-auth

In v6 of libs, the `@onecx/keycloak-auth` package has been removed and replaced with `@onecx/angular-auth`.

## [](#update-module-imports)Update module imports

* Install the `@onecx/angular-auth` package (if not already installed)  
```bash  
npm install @onecx/angular-auth  
```
* Replace all imports of `KeycloakAuthModule` from `@onecx/keycloak-auth` with `AngularAuthModule` from `@onecx/angular-auth`.
* Replace `KeycloakAuthModule` with `AngularAuthModule`.

### [](#%5Fexample)Example

Before

```typescript
import { KeycloakAuthModule } from '@onecx/keycloak-auth';

@NgModule({
  imports: [
    KeycloakAuthModule
  ]
})
export class AppModule {}
```

After

```typescript
import { AngularAuthModule } from '@onecx/angular-auth';

@NgModule({
  imports: [
    AngularAuthModule
  ]
})
export class AppModule {}
```

## [](#update-packages)Update Packages

After removing `@onecx/keycloak-auth`, `keycloak-angular` is no longer required and can be removed (unless your application still uses it directly). Update your dependencies as follows:

Uninstall the deprecated packages

```bash
npm uninstall --save @onecx/keycloak-auth
npm uninstall --save keycloak-angular
```

| |  If you use Keycloak as your identity provider and want to keep using it with the new authentication module, you may need to install keycloak-js. Check whether your application still requires keycloak-js by referencing [Remove keycloak-js](../angular-20/remove-keycloak-js.html). If it is required, install it: npm install keycloak-js |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
