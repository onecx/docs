# Migrate a vanilla Angular app to OneCX

This page walks a fresh (non-OneCX) Angular app to the current OneCX end-state. It keeps the migration focused on the v8 baseline and links out to the setup pages instead of restating their steps. If the application has not yet been migrated to OneCX, first use the [legacy migration guide](../angular/app-to-onecx.html) to integrate it with the OneCX library version compatible with its current Angular version. Then follow the version-specific upgrade guides to reach the current OneCX version.

## [](#general)General

### [](#prerequisites)Prerequisites

This page assumes that an Angular project is already set up and that a OneCX platform instance is up and running. The target is the current end-state: an Angular application on Angular 21, built against the OneCX platform libraries version 8\. If your app is on an older Angular version, upgrade it to Angular 21 first.

The required Angular version and compatible shared package versions are documented in [Platform & Package Compatibility Requirements](../setup/required/platform-package-compatibility.html). Complete the [Required Setup](../setup/required/index.html) before following this guide; this page does not restate the install steps.

Note that this page does not cover general Angular project setup or the steps to configure OneCX.

## [](#migration-steps)Setup steps

The goal of this setup is to transform a "vanilla" Angular app into a OneCX compatible app that exposes a microfrontend which can be loaded and displayed by the OneCX platform. The steps have been tested in fresh Angular apps generated with the Angular CLI and the Nx CLI (using Webpack as a bundler). Some steps only apply to either Angular CLI or Nx-based applications and are marked accordingly.

### [](#ensure-functionality)Ensure that your application works as expected

Before starting, verify that the application works in its pre-migration state by running its tests, building it, and running it in a browser. This helps prevent unexpected errors in later stages.

### [](#refactor-angular-json)Refactor `angular.json` for Angular CLI apps (Only Angular CLI)

To correctly bundle an app for use in a microfrontend context, Angular CLI applications should use `ngx-build-plus` builders. See <https://github.com/manfredsteyer/ngx-build-plus> for the official project.

Add the `node_modules/@webcomponents/webcomponentsjs/webcomponents-bundle.js` script to the build configuration and keep the rest of the Module Federation setup aligned with [Module Federation](../concepts/module-federation.html) and [Web Components in OneCX](../../onecx-docs-overview/module-federation/webcomponents.html).

### [](#refactor-project-json)Configure `project.json` for Nx apps (Only NX)

Nx applications should use a Webpack-based builder such as `@nx/angular:webpack-browser`. See <https://nx.dev/technologies/angular/api/executors/webpack-browser> for the official Nx Angular executor reference.

Other Nx builders can be chosen; they must still include the `node_modules/@webcomponents/webcomponentsjs/webcomponents-bundle.js` script and support the Module Federation and Web Components requirements described above.

### [](#create-entrypoints)Create the app entrypoint files

To enable an app to run both as a standalone application and as a microfrontend, it must expose the entrypoint files that bootstrap the remote module: the `DoBootstrap` module, the `createAppEntrypoint` call, the `initializeRouter` provider, the `startsWith` route matcher, and `PortalApiConfiguration`. These entrypoint files have a home page — see [Expose a Remote Module (Module Approach)](../setup/required/expose-remote-module/module-approach.html) — and are not restated here.

### [](#webpack-configuration)Configure the Webpack `shared` scope

A fresh app must assign itself and its shared dependencies to the correct Module Federation share scope and choose which packages to share. That configuration has a home page — see [Configure Remote Package Sharing](../setup/required/configure-remote-package-sharing.html) — and is not restated here. As a starting point, the fresh app shares the Angular framework packages and the OneCX packages it depends on, and exposes `remoteEntry.js` with the `uniqueName` set to its microfrontend name and `publicPath` set to `auto`.

### [](#environment-file)Add environment file `env.json`

During the loading of an app, OneCX will try to load its environment file. To avoid any errors, a file called `env.json` should be accessible at <http://localhost:4200/assets/env.json>. This can be achieved by adding the respective file to the assets folder of the application. The file can be used to pass environment variables to OneCX. For now it can just contain an empty object (`{}`).

### [](#test-remote-entrypoint)Verify that the app is exposing a remote entry point

The important outcome is a Module Federation build that exposes `remoteEntry.js` for the OneCX shell to load; see the [Module Federation](../concepts/module-federation.html) and [Web Components in OneCX](../../onecx-docs-overview/module-federation/webcomponents.html) guides. After starting the application with its start command (e.g. `npm start`), the application’s entrypoint file (`remoteEntry.js`) should be accessible at <http://localhost:4200/remoteEntry.js>.

## [](#v8-setup-checklist)v8 setup checklist

Reach the following home pages, in order, to complete the OneCX setup for the fresh app. Each page owns the step; this page links out rather than restating it.

1. [Platform & Package Compatibility Requirements](../setup/required/platform-package-compatibility.html) — the Angular 21 / libs 8.x baseline and the compatible shared package versions.
2. [Expose a Remote Module](../setup/required/expose-remote-module.html) — expose the app’s module via Module Federation so the shell can load it (see the [Module Approach](../setup/required/expose-remote-module/module-approach.html)).
3. [Configure Remote Package Sharing](../setup/required/configure-remote-package-sharing.html) — assign the app and its shared dependencies to the correct share scope.
4. [Configure Authentication](../setup/required/configure-authentication.html) — ensure requests carry the shell’s authentication header, and keep the app clear of the shell’s IDP client.
5. [PrimeNG](../setup/required/primeng/primeng.html) — add the required Webpack `ModifySourcePlugin` config when the app uses PrimeNG.
6. [Material](../setup/required/material/material.html) — add the required Webpack `ModifySourcePlugin` config when the app uses `@angular/material` or `@angular/cdk`.
7. [Apply Theming](../setup/recommended/apply-theming.html) — let the shell load and apply the theme globally; do not load it in the app.
8. [PrimeNG Theming Customization](../features/primeng/theming-customization.html) — register `provideThemeConfig()` for PrimeNG in microfrontends and remote components.
9. [Multi-language Translations](../angular/translation/multi-language-setup.html) — set up `OnecxTranslateLoader` and the translation connection service.
10. [Expose Component Styles (Angular)](../setup/recommended/expose-component-styles/angular.html) — expose a stable `styles.css` and the OneCX library styles in the build output.

## [](#standalone-mode)Standalone Mode

After completing the steps above, a previously existing "vanilla" Angular application can be run as a microfrontend in OneCX. If the app additionally has to support running standalone (e.g. in local development), see [Enable OneCX app to run in standalone](../angular/standalone.html).

## [](#further-reading)Further Reading

For more information on how OneCX loads microfrontends and utilizes web components for content rendering, refer to the [Microfrontend Content Loading in OneCX](../../onecx-docs-overview/module-federation/microfrontend-content-loading.html) and [Web Components in OneCX](../../onecx-docs-overview/module-federation/webcomponents.html) pages of the OneCX Docs.

## [](#troubleshooting)Troubleshooting

See the [Troubleshooting](../troubleshooting/index.html) section for the preparation steps, common causes, and named errors to work through when the app does not load, route, or render as expected.
