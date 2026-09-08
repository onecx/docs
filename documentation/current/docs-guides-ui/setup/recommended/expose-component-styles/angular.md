# Expose Component Styles in Angular Applications

This page covers exposing an Angular application’s and its OneCX libraries' styles in the build output. See [Expose Component Styles](../expose-component-styles.html) for why this matters.

## [](#angular-expose-app-styles)Expose App styles.css

The application must expose its own `styles.css` in the build output. How this is done depends on the build tool used:

Nx (project.json)

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

Because the generated stylesheet filename normally includes a content hash, adjust the build command to rename it to a stable `styles.css`:

package.json build output

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

Verify that `styles.css`, including all of the app’s styles, is present in the build output before deploying.

## [](#angular-expose-library-styles)Expose Library Styles

If the application uses OneCX libraries that ship their own stylesheets, expose those stylesheets in the build configuration as well — otherwise components sourced from those libraries render with incorrect styles.

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
