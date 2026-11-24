# Upgrade NX Application to Angular 22

This guide describes how to upgrade an NX-based OneCX application to Angular 22\. Complete the pre-migration steps from the main migration guide (in particular [Migrate the application’s own PrimeNG usage to Optimus UI v1](migrate-to-optimus-ui-v1.html)) before continuing.

| |  The OneCX UI libraries v9 ship with this upgrade. The toolchain step and the [v9 libraries bump](update-onecx-libs-v9.html) are part of the same upgrade — do not leave the toolchain on Angular 22 while the @onecx/\* packages stay on v8. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#%5Fupdate%5Fonecxnx%5Fplugin)Update @onecx/nx-plugin

Update `@onecx/nx-plugin` to the Nx 23 line, alongside the `nx`/@nx/ packages. `@onecx/nx-plugin` is versioned independently of the `@onecx/` libs in this repository, so it does not follow the libs `^9.0.0` scheme — install the Nx 23 release of the plugin matching the `nx`/`@nx/*` versions the workspace pins (the OneCX Shell Angular 22 preloader uses `23.3.0`): 

```bash
npm install @onecx/nx-plugin@<version>
```

| |  Like @onecx/nx-plugin@^22.1.3 in the [Angular 21 guide](../angular-21/update-nx-angular-version-21.html), the Nx 23 line of @onecx/nx-plugin is not published to the public npm registry. Install it from the registry that the @onecx/\* packages are resolved from. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

## [](#%5Fupdate%5Fnx%5Fand%5Fangular%5Fpackages)Update NX and Angular packages

Update the Angular and NX packages in the workspace by running:

```bash
nx migrate latest --interactive
```

Apply all proposed updates up to Angular 22.

For details on NX / Angular compatibility, refer to the [Angular NX Version Matrix](https://nx.dev/docs/technologies/angular/guides/angular-nx-version-matrix).

For details on `nx migrate`, refer to the official documentation: [NX Migrate Documentation](https://nx.dev/docs/guides/tips-n-tricks/advanced-update).

If the project is not an NX workspace, follow the official Angular update guide to perform the version upgrade: [Angular Update Guide](https://angular.dev/update-guide?v=21.0-22.0).

## [](#%5Fupdate%5Fpackage%5Fversions%5Fin%5Fpackage%5Fjson)Update package versions in `package.json`

1. Update the packages to the versions listed in the table below.
2. After updating `package.json`, run `npm install` to install the new versions. If peer dependency errors appear, update the affected packages to compatible versions.

| Package     | Required Version | Notes                          |
| ----------- | ---------------- | ------------------------------ |
| @angular/\* | ^22.2.3          | All Angular framework packages |
| typescript  | \~6.0.2          | TypeScript 6                   |
| zone.js     | \~0.16.0         | Zone.js for Angular 22         |
| nx, @nx/\*  | 23.x             | NX 23 for Angular 22           |

| |  If dependency conflicts that reference old versions persist, reinstall dependencies from scratch: rm -rf node\_modules package-lock.json .angular dist \~/.angular/cache && npm cache clean --force && npm install |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| |  Make sure to migrate the updated packages and resolve any breaking changes. Refer to the official documentation of each package for migration guides and instructions. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#%5Frun%5Fnx%5Fmigration)Run NX migration

After updating package versions, run:

```bash
nx migrate --run-migrations
```

| |  While applying the toolchain update, keep the @angular-devkit/build-angular and webpack pins documented in [Keep build-angular at 22.2.3 and webpack at 5.111.0](keep-build-angular-22-2-3-and-webpack.html). |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

After this step, proceed with the remaining migration steps, starting with [Update the OneCX UI libraries to v9](update-onecx-libs-v9.html).

## [](#%5Fcleanup%5Fmigration%5Fdependencies)Cleanup Migration Dependencies

After completing all migration steps, remove migration-only dependencies that are no longer required:

```bash
npm uninstall @onecx/nx-migration-utils @nx/devkit
```

| |  @onecx/nx-migration-utils is removed entirely in v8 (the package itself is no longer published); this uninstall is mandatory, not optional cleanup. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ |
