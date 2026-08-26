# Upgrade NX Application to Angular 21

This guide describes how to upgrade an NX-based OneCX application to Angular 21\. Complete the pre-migration steps from the main migration guide before you continue.

## [](#%5Fupdate%5Fonecxnx%5Fplugin)Update @onecx/nx-plugin

Update `@onecx/nx-plugin` to latest 8.x.y available.

```bash
npm install @onecx/nx-plugin@^8
```

## [](#%5Fupdate%5Fnx%5Fand%5Fangular%5Fpackages)Update NX and Angular packages

Update the Angular and NX packages in your workspace by running:

```bash
nx migrate latest --interactive
```

Apply all proposed updates up to Angular 21.

For details on NX / Angular compatibility, refer to the [Angular NX Version Matrix](#https://nx.dev/docs/technologies/angular/guides/angular-nx-version-matrix).

For details on `nx migrate`, refer to the official documentation: [NX Migrate Documentation](#https://nx.dev/docs/guides/tips-n-tricks/advanced-update).

## [](#%5Fupdate%5Fpackage%5Fversions%5Fin%5Fpackage%5Fjson)Update package versions in `package.json`

1. Update all used `@onecx/*` packages to version `^8.0.0`.  
Example:  
```json  
npm install @onecx/<package-name>@^8  
```
2. Update the packages listed here to the specified versions: [Required Package Updates](update-v8-packages.html).
3. After updating `package.json`, run `npm install` to install the new versions. If you see peer dependency errors, update the affected packages to compatible versions.

| |  If you still see dependency conflicts that reference old versions, reinstall dependencies from scratch: rm -rf node\_modules package-lock.json .angular dist \~/.angular/cache && npm cache clean --force && npm install |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| |  Make sure to migrate the updated packages and resolve any breaking changes. Refer to the official documentation of each package for migration guides and instructions. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#%5Frun%5Fnx%5Fmigration)Run NX migration

After updating package versions, run:

```bash
nx migrate --run-migrations
```

After this step, proceed with the remaining post-migration steps.

## [](#%5Fcleanup%5Fmigration%5Fdependencies)Cleanup Migration Dependencies

After completing all migration steps, remove migration-only dependencies that are no longer required:

```bash
npm uninstall @onecx/nx-migration-utils @nx/devkit
```
