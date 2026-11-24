# Import shared library configuration helpers from <code>@onecx/build-utils</code>

In OneCX UI libraries v9, `@onecx/accelerator` no longer exports the Module Federation helpers `getOneCXSharedLibraryConfig` and `getOneCXSharedRecommendations`. They are only available from `@onecx/build-utils`.

`@onecx/build-utils` is already published for v8 (since 8.7.0) with the same functions, so the imports can be switched before upgrading to Angular 22.

## [](#%5Frequired%5Fchange)Required change

1. Install `@onecx/build-utils` as a dev dependency, using the same version as the other `@onecx/*` libraries:  
```bash  
npm install @onecx/build-utils@^8 --save-dev  
```
2. Update the imports in the Module Federation or webpack configuration:  
```javascript  
// before  
const { getOneCXSharedLibraryConfig } = require('@onecx/accelerator')  
// after  
const { getOneCXSharedLibraryConfig } = require('@onecx/build-utils')  
```

The function signatures are unchanged. For usage details, see [@onecx/build-utils](../../libraries/build-utils.html).

| |  In v9, the shared library recommendations treat @openng/optimus-ui packages as shared libraries instead of primeng packages. No change in the configuration is needed for this. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
