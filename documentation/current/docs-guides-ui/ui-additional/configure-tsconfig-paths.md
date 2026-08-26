# Configure TypeScript Path Aliases (tsconfig paths)

TypeScript path aliases ("tsconfig paths") are defined in the root `tsconfig.json` of a OneCX compatible UI App. Aliases shorten imports and improve readability.

## [](#why-configure-tsconfig-paths)Why configure tsconfig paths?

Aliases replace long relative imports (for example, `../../../shared/components`) with stable names (for example, `@shared/components`). This improves readability and reduces refactoring when files move.

## [](#tsconfig-paths-types)Types of tsconfig paths

Two common patterns are used:

### [](#wildcard-paths)Wildcard paths

Wildcard paths map an alias prefix to a folder. Use this pattern for importing multiple modules from the mapped folder.

```json
{
    "compilerOptions": {
        "baseUrl": "./",
        "paths": {
            "@custom-path/*": ["src/app/custom-folder/*"]
        }
    }
}
```

### [](#specific-paths)Specific paths

Specific paths map one exact import to a single file (often a barrel file). Only the exact import `@custom-path` is mapped; `@custom-path/custom.component` does not match.

```json
{
    "compilerOptions": {
        "baseUrl": "./",
        "paths": {
            "@custom-path": ["src/app/custom-folder/index.ts"]
        }
    }
}
```

## [](#potential-issues-in-onecx-compatible-apps)Potential issues in OneCX-compatible apps

### [](#webpack-module-resolution)Webpack module resolution

OneCX-compatible UI Apps use Webpack (module federation). TypeScript path aliases are defined in `tsconfig.json`, but Webpack does not read them unless configured.

#### [](#error-cannot-find-module)Error: Cannot find module

If Webpack cannot resolve an import such as `@custom-path/…​`, errors like `Cannot find module '@custom-path'` may occur. See [TsconfigPathsPlugin](#tsconfig-paths-plugin).

### [](#alias-conflicts)Alias conflicts

Alias names that overlap with existing imports used by a OneCX-compatible UI App (or its dependencies) can cause unexpected resolution and type errors.

#### [](#error-cannot-find-module-or-type-errors)Error: Cannot find module (or type errors)

Conflicts can show up as `Module not found: Error: Can’t resolve …​` or as TypeScript resolving to the wrong file. Use unique, descriptive aliases that do not overlap with existing package names.

### [](#usage-of-incorrect-alias-type)Usage of incorrect alias type

Using specific paths when wildcard paths are needed (or vice versa) can lead to resolution errors in imports.

#### [](#cannot-find-module-or-its-corresponding-type-declarations)Cannot find module or its corresponding type declarations

Imports must match the alias pattern (wildcard vs specific). If they don’t, TypeScript reports `Cannot find module …​` (for example `@custom-path` vs `@custom-path/custom.component`). Use the correct alias type. See [Types of tsconfig paths](#tsconfig-paths-types).

## [](#angular-cli-nx-app-configuration)Angular CLI / Nx App Configuration

Angular CLI’s Webpack-based build integrates TypeScript path mapping into module resolution. In most cases, path aliases work without duplicating them in a custom Webpack configuration.

## [](#react-app-configuration-and-other-non-angular-apps)React App Configuration (and other non-Angular apps)

For React apps (and other non-Angular setups), the bundler may not apply `tsconfig.json` path aliases automatically. Webpack configuration is typically required.

### [](#tsconfig-paths-plugin)Recommended Approach: Use TsconfigPathsPlugin

1. Install the plugin:  
```bash  
npm install --save-dev tsconfig-paths-webpack-plugin  
```
2. In `webpack.config.js`, import the plugin:  
```js  
const TsconfigPathsPlugin = require('tsconfig-paths-webpack-plugin');  
```
3. Register the plugin in `resolve.plugins`:  
```js  
module.exports = {  
    // ... other webpack configuration options ...  
    resolve: {  
        // ... other resolve options ...  
        plugins: [  
            new TsconfigPathsPlugin({  
                configFile: './tsconfig.json'  
            })  
        ]  
    }  
};  
```

Alternatively, aliases can be duplicated in Webpack via `resolve.alias` (see [Webpack documentation](https://webpack.js.org/configuration/resolve/#resolvealias)). This is less maintainable because manual synchronization with `tsconfig.json` is required.

## [](#best-practices)Best Practices

Recommended practices:

* Use unique, descriptive aliases to avoid conflicts with packages used in OneCX-compatible apps.
* Use an `@` prefix to make custom aliases explicit.
* Group related aliases and remove unused entries periodically.
* Avoid aliases for shared libraries consumed across multiple microfrontends. Module federation and bundlers can resolve them differently.
