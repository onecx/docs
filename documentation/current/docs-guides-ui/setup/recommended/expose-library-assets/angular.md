# Expose Library Assets in Angular Applications

This page covers exposing the static assets of the OneCX libraries an Angular application depends on. See [Expose Library Assets](../expose-library-assets.html) for why this matters.

If the application uses OneCX libraries, confirm their assets (e.g. i18n files) are exposed and available in the build output — otherwise assets shipped by those libraries are missing. Nx workspaces commonly configure the assets array in the application’s `project.json`; Angular CLI workspaces configure the same assets array under the project’s build target in `angular.json`.

Nx project.json assets configuration

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
      },
      // @onecx/angular-accelerator
      {
        "glob": "**/*",
        "input": "./node_modules/@onecx/angular-accelerator/assets/",
        "output": "/onecx-angular-accelerator/assets/"
      },
      // @onecx/angular-utils
      {
        "glob": "**/*",
        "input": "./node_modules/@onecx/angular-utils/assets/",
        "output": "/onecx-angular-utils/assets/"
      },
      ...
    ],
    ...
  }
...
```

Angular CLI angular.json assets configuration

```json
...
  "projects": {
    "<project-name>": {
      ...
      "architect": {
        "build": {
          "options": {
            ...
            "assets": [
              ...
              // @onecx/portal-integration-angular
              {
                "glob": "**/*",
                "input": "node_modules/@onecx/portal-integration-angular/assets/",
                "output": "/onecx-portal-lib/assets/"
              },
              // @onecx/angular-accelerator
              {
                "glob": "**/*",
                "input": "./node_modules/@onecx/angular-accelerator/assets/",
                "output": "/onecx-angular-accelerator/assets/"
              },
              // @onecx/angular-utils
              {
                "glob": "**/*",
                "input": "./node_modules/@onecx/angular-utils/assets/",
                "output": "/onecx-angular-utils/assets/"
              },
              ...
            ]
          }
        }
      }
    }
  }
...
```
