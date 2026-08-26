# undefined

## [](#onecxSharedRecommendations)OneCX Shared Recommendations

The `getOneCXSharedRecommendations` function provides OneCX-specific recommendations for shared library configurations. It automatically applies optimized settings for Angular, OneCX, RxJS, PrimeNG, ngx-translate, and ngrx packages.

```ts
getOneCXSharedRecommendations(
  libraryName: string,
  sharedConfig: SharedLibraryConfig
): false | SharedLibraryConfig
```

### [](#onecxSharedRecommendationsUsage)Usage Example

```ts
import { getOneCXSharedRecommendations } from '@onecx/build-utils';

const sharedConfig = {
  singleton: false,
  strictVersion: false,
  eager: false,
  requiredVersion: 'any',
  shareScope: 'angular_21'
};

const recommendedConfig = getOneCXSharedRecommendations('@angular/core', sharedConfig);
// Output: { singleton: false, strictVersion: false, eager: false, version: '1.0.0', requiredVersion: 'any', shareScope: 'angular_21' }
```

### [](#configProperties)Config Properties

The `SharedLibraryConfig` object can include the following properties:

| Property           | Type            | Description                                              |
| ------------------ | --------------- | -------------------------------------------------------- |
| singleton          | boolean         | Whether only one instance should exist                   |
| strictVersion      | boolean         | Whether version mismatches should cause errors           |
| eager              | boolean         | Whether to load immediately vs lazy                      |
| requiredVersion    | string \| false | Required version or any/false for no requirement         |
| version            | string          | Actual version of the package                            |
| includeSecondaries | boolean         | Include secondary entry points (for @angular-architects) |
| shareScope         | string          | Scope for sharing (e.g., angular\_21)                    |

For recommended libraries, the function applies the following defaults:

* `singleton`: `false` — Allows multiple versions to coexist
* `strictVersion`: `false` — Permits version flexibility
* `eager`: `false` — Enables lazy loading of shared modules
