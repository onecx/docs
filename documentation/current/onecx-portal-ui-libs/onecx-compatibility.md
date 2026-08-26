# OneCX UI Libraries: Compatibility

This guide lists the minimal requirements for an UI App to be fully compatible with OneCX. Each requirement is classified as "must-have" or "should-have" and the impact of missing each requirement is described.

## [](#must-have-requirements)Must-have Requirements

Have lower Angular package version than the Shell or respective preloader

Impact: Broken environment

* Check the Shell version and ensure your App uses an equal or lower Angular version.
* Please refer to this [Troubleshooting Guide shell related section](../onecx-docs-dev/troubleshooting.html#shell-related) on how to use DevTools to inspect shared packages.

Constructed using @onecx/angular-webcomponents

Impact: Router out of sync, many potential issues

* For step-by-step instructions on migrating a vanilla Angular App to a OneCX-compatible microfrontend using @onecx/angular-webcomponents among other packages, refer to the [Migration Steps in Vanilla to OneCX Migration Guide](../docs-guides-ui/angular/app-to-onecx.html#migration-steps).

Module-federation with remoteEntry.js (any technology)

Impact: Applications exposed with different technologies might not be compatible with the Shell

* Ensure your App exposes remoteEntry.js and is configured for module federation.

Expose assets of used libraries

Impact: Translations missing

* Confirm assets (e.g., i18n) from libraries are exposed and available in your build output.
* Include the assets of the libraries they use in the angular.json or project.json file.

Example assets configuration

```json
...
  "build": {
    ...
    "assets": [
      ...
      // @onecx/portal-integration-angular
      {
        "glob": "**/*",
        "input": "node_modules/@onecx/portal-integration-angular/assets/",
        "output": "/onecx-portal-lib/assets/"
      }
      // @onecx/angular-accelerator
      {
        "glob": "**/*",
        "input": "./node_modules/@onecx/angular-accelerator/assets/",
        "output": "/onecx-angular-accelerator/assets/"
      }
      // @onecx/angular-utils
      {
        "glob": "**/*",
        "input": "./node_modules/@onecx/angular-utils/assets/",
        "output": "/onecx-angular-utils/assets/"
      }
      ...
    ],
    ...
  }
...
```

Expose styles.css of used libraries

Impact: Styles of components from libraries might be incorrect

* Expose library styles in project.json or angular.json.

Example styles configuration

```json
...
  "build": {
    ...
    "styles": [
      ...
      // @onecx/portal-integration-angular
      "node_modules/@onecx/portal-integration-angular/assets/styles.scss",

      // @onecx/angular-accelerator
      "node_modules/@onecx/angular-accelerator/assets/styles.scss",
      ...
    ],
    ...
  }
...
```

Sharing is done with '^'

Impact: We should share as much as possible

* Use caret '^' for all shared package versions in package.json (except rxjs, which should use '\~').
* Refer to the [Troubleshooting Guide installed packages section](../onecx-docs-dev/troubleshooting.html#installed-packages) for correct range and examples.

Angular, PrimeNG, NGRX and OneCX packages are shared

Impact: Broken application

* In webpack.config.js, share all required packages
* Refer to the [Troubleshooting Guide webpack config section](../onecx-docs-dev/troubleshooting.html#webpack-configuration) for correct sharing syntax and examples.

Share @onecx/angular-utils library

Impact: Might lead to unwanted side effects for your App and also other Apps in the Shell.

* Especially if @onecx/angular-accelerator or @onecx/portal-integration-interface is used and shared.
* Please check your webpack configuration and make sure to include the @onecx/angular-utils in the shared modules.

Routing is done with relative paths

Impact: Incorrect routing results

* Use relative paths in Angular router configuration to avoid navigation issues.
* Please refer to the [OneCX Routing Guide](../docs-guides-ui/angular/routing/index.html#general-routing-guidelines) for using relative paths and other information on routing in OneCX.

Webpack configuration for importMeta

Impact: Translation issues

* Ensure your webpack configuration includes the correct importMeta configuration.
* For the correct configuration, please refer to the [OneCX Multi-language Translations Guide](../docs-guides-ui/angular/translation/multi-language-setup.html#provide-translation-path) and other information on multi-language in OneCX.

Ensure package compatibility

Impact: Broken application

* Verify that all packages used in your App are compatible with OneCX.

__Table 1\. Compatible package versions for Angular 18 (libs version 5.x)__
| Package             | Compatible Versions |
| ------------------- | ------------------- |
| @ngx-translate/core | ^15.0.0             |
| ngx-build-plus      | ^18.0.0             |
| primeng             | ^17.18.0            |

__Table 2\. Compatible package versions for Angular 19 (libs version 6.x)__
| Package             | Compatible Versions |
| ------------------- | ------------------- |
| @ngx-translate/core | ^16.0.0             |
| ngx-build-plus      | ^19.0.0             |
| primeng             | ^19.0.0             |

## [](#should-have-requirements)Should-have Requirements

Module-federation via webpack for exposing remoteEntry.js

Impact: We don’t know if other technologies are working

* Prefer webpack for module federation setup.
* Verify your webpack configuration:

Example webpack.config.js

```js
...
const config = withModuleFederationPlugin({
  name: 'YOUR_MFE_NAME',
  filename: 'remoteEntry.js',
  exposes: {
    './RemoteModule': 'src/main.ts',
  },
  shared: share({...})
});
...
```

Expose App styles.css

Impact: No styles for the application are loaded

* Ensure your App exposes its styles.css.
* How the styles.css is exposed depends on the package used for building the App (NX or Angular CLI).
* NX:

project.json

```json
{
    ...
    "styles": [
        {
            "input": "./src/styles.scss",
            "bundleName": "styles",
            "inject": true
        }
    ],
    ...
}
```

* Angular CLI:

package.json

```json
{
  ...
  "scripts": {
    "postbuild": "mv \"$(find dist/my-project-name -maxdepth 1 -type f -name 'styles.*.css' | head -n 1)\" dist/my-project-name/styles.css",
  }
  ...
}
```

* Adjust the build command in package.json to rename the generated styles file to styles.css because of the hash in the filename by adding`cp dist/replace_path_to/styles.*.css dist/replace_path_to/styles.css"`
* Ensure the styles.css including all your styles is present in the build output.

Example package.json

```json
{
  ...
  "scripts": {
    ...
    "build": "nx build && cp dist/my-project-name/styles.*.css dist/my-project-name/styles.css",
    ...
  }
  ...
}
```
