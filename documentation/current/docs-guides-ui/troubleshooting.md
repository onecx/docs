# Troubleshooting UI Issues

This page provides assistance in resolving common UI problems in OneCX.

## [](#preparation)Preparation

### [](#ui-compatibility)UI Compatibility

Make sure that the App is compatible as documented in [OneCX UI Compatibility](../onecx-portal-ui-libs/onecx-compatibility.html).

### [](#improve-debugging-experience)Improve debugging experience

To understand the root cause of issues, it is recommended to enable source maps in the application and shell during development. For more information on how to enable source maps, see [Enable source maps guide](ui-additional/enable-source-maps.html).

## [](#general-issues)General issues

### [](#webpack-configuration)Package sharing

Common issues arise when the shared packages list is not complete or when the versions of the shared packages are not compatible. To verify correct package sharing, check the [package sharing](../onecx-portal-ui-libs/onecx-compatibility.html#package-sharing) documentation and verify all technology dependent requirements in the [OneCX UI Compatibility](../onecx-portal-ui-libs/onecx-compatibility.html) guide.

### [](#clean-install-build)Clean Install and Build

Sometimes, issues can be resolved by performing a clean install and build of the application. This involves removing caches, recreating dependencies, clearing the npm cache, and reinstalling all packages. Do a clean install and build of the App:

* Remove caches (like .angular and .nx folder)
* Recreate dependencies (node\_modules and package-lock.json)
* Run following command to clear the npm cache:

  npm cache clean --force

* Install all packages:

  npm install

* Build and run the App

## [](#application-setup)Application Setup

Make sure that the application is set up correctly to work in the environment. Regardless of the used local development strategy, the following should be checked:

* exposedModule is set to the correct module name
* tagName is set to the correct tag name
* remoteEntry url is set to the correct url

Depending on the used local development strategy, those values should be set in different places (data imports for local environment, values.yaml of the application, manual configuration on the OneCX platform via Application Store and Workspace UIs).

## [](#shell-compatibility)Shell compatibility Issues

Incorrect package sharing between the shell and the application can lead to issues. To verify available major version of packages in the shell, check the [Shell version information](../onecx-shell-ui/onecx-shell-ui-docs.html#shell-version-information) documentation.

## [](#specific-issues)Specific Issues

### [](#rendering-priority)Rendering priority

In some cases, elements may not be displayed correctly. This can have multiple reasons, however below are some common issues that can be checked to resolve the problem.

#### [](#z-index-issues)Z-index issues

Since every microfrontend can use its own CSS and be built on different technology stacks, it is possible that the z-index of elements is not working as expected. To resolve issues where elements are not displayed according to expectations (e.g. a modal is not displayed on top of other elements), check the following:

* z-index of the element that should be displayed on
* z-index of the element that is displayed on top of the other element

If possible, the z-index of the element controlled by the application having the issue should be adjusted. In case this is not an option, please reach out to the OneCX support team for assistance.

### [](#webpack-compilation)The 'compilation' argument must be an instance of Compilation

Errors indicating issues with webpack compilation are related to multiple versions used in the project. To fix the issue:

* run `npm ls webpack`
* identify packages with different webpack version
* ensure only 1 version of webpack is present

To use only 1 version of webpack, please adjust the versions of the packages that depend on webpack to use the same version. Its possible by updating the package.json file to specify compatible versions or by using npm overrides feature.

### [](#angular-compilation)Application is not showing up and "t is not a function" error is in console

If the application is not showing up and errors like `t is not a function` are in the console, then most likely the builder and the Angular packages used in the project are not compatible. To resolve the issue:

* make sure that the builder used in the project is compatible with the Angular version used  
   * e.g. for Angular 18 and ngx-build-plus package use version `^18.0.0`

### [](#tsconfig-path-mapping)Tsconfig Path Alias Mapping Errors

For more information on how to configure tsconfig paths, refer to [Configure tsconfig paths documentation](ui-additional/configure-tsconfig-paths.html).

#### [](#error-cannot-find-module-build-error)Error: Cannot find module (build error)

**Problem**: If Webpack cannot resolve an import such as `@custom-path/…​`, errors like `Cannot find module '@custom-path'` may occur.

**Solution**: To fix this, please configure Webpack to understand TypeScript path aliases. See [Webpack path aliases configuration](ui-additional/configure-tsconfig-paths.html#tsconfig-paths-plugin).

#### [](#error-cannot-find-module-or-type-errors-for-imports-that-worked-before-paths-configuration)Error: Cannot find module or type errors (for imports that worked before paths configuration)

**Problem**: Conflicts can show up as `Module not found: Error: Can’t resolve …​` or as TypeScript resolving to the wrong file.

**Solution**: Use unique, descriptive aliases that do not overlap with existing package names.

#### [](#cannot-find-module-or-its-corresponding-type-declarations-editor-error-on-import)Cannot find module or its corresponding type declarations (editor error on import)

**Problem**: Imports must match the alias pattern (wildcard vs specific). If they don’t, TypeScript reports `Cannot find module …​` (for example `@custom-path` vs `@custom-path/custom.component`).

**Solution**: Use the correct alias type. See [Types of tsconfig paths](ui-additional/configure-tsconfig-paths.html#tsconfig-paths-types).
