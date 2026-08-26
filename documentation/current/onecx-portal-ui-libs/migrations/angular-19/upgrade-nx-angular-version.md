# Upgrade NX Application to Angular 19

This guide describes how to upgrade an NX-based OneCX application to Angular 19\. Complete the pre-migration steps from the main migration guide before you continue.

## [](#%5Fupdate%5Fonecxnx%5Fplugin)Update @onecx/nx-plugin

Update `@onecx/nx-plugin` to latest 6.x.y available.

```bash
npm install @onecx/nx-plugin@^6
```

## [](#%5Fupdate%5Fnx%5Fpackages)Update NX Packages

Update the Angular and NX packages in your workspace by running:

```bash
nx migrate 20.4.0 --interactive
```

This command prompts you to apply updates for each major version of Angular and TypeScript. Apply all proposed updates up to Angular 19.1 and TypeScript 5.7.

For details on NX / Angular compatibility, refer to the [Angular NX Version Matrix](https://nx.dev/docs/technologies/angular/guides/angular-nx-version-matrix).

For details on `nx migrate`, refer to the official documentation: [NX Migrate Documentation](https://nx.dev/docs/guides/tips-n-tricks/advanced-update).

## [](#%5Fupdate%5Fpackage%5Fversions%5Fin%5Fpackage%5Fjson)Update Package Versions in package.json

1. After running the migration command, update the remaining packages manually. Update all `@onecx/*` packages to latest available `6.x.y` version.  
Example:  
```json  
npm install @onecx/<package-name>@^6  
```
2. Update the packages listed here to the specified versions: [Required Package Updates](update-packages.html).
3. The following packages should be removed:  
   * `@onecx/keycloak-auth` \- Follow the instructions in [Remove @onecx/keycloak-auth](remove-keycloak-auth.html) to update your application accordingly.  
   * `@onecx/portal-layout-styles`  
   * `@onecx/portal-integration-angular`
4. After updating `package.json`, run `npm install` to install the new versions. If you see peer dependency errors, update the affected packages to compatible versions.

| |  If you still see dependency conflicts that reference old versions, reinstall dependencies from scratch: rm -rf node\_modules package-lock.json .angular dist \~/.angular/cache && npm cache clean --force && npm install |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| |  Make sure to migrate the updated packages and resolve any breaking changes. Refer to the official documentation of each package for migration guides and instructions. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#%5Frun%5Fnx%5Fmigration)Run NX Migration

After updating the package versions, run the following command to apply the generated migrations:

```bash
nx migrate --run-migrations
```

After this step, proceed with the remaining post-migration steps.
