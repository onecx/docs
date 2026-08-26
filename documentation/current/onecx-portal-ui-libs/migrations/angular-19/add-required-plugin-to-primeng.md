# Add Webpack Plugin for PrimeNG

In OneCX version 6 uses PrimeNG 19 and requires applications to add a Webpack plugin. This change is required after upgrading to Angular 19.

| |  This setup will be replaced by a OneCX-provided Webpack plugin in a future version. |
| -------------------------------------------------------------------------------------- |

## [](#%5Finstall%5Fand%5Fconfigure%5Fthe%5Fwebpack%5Fplugin)Install and Configure the Webpack Plugin

1. Install `modify-source-webpack-plugin` compatible with Webpack 5:  
```bash  
npm install modify-source-webpack-plugin@^4 --save-dev  
```
2. Import `ModifySourcePlugin` and `ReplaceOperation` from `modify-source-webpack-plugin` in `webpack.config.js`
3. Create a `modifyPrimeNgPlugin` instance with a rules array containing one rule object:  
   * The rule must define a `test` function that returns `true` when `module.resource` exists and the resource path includes `primeng`.  
   * The rule must include an `operations` array with a `ReplaceOperation` configured with:  
         * scope: `all`  
         * match pattern: `document\.createElement\(([^)]+)\)`  
         * replacement: `document.createElementFromPrimeNg({"this": this, "arguments": Array.from(arguments), element: $1})`  
   * The rule must also include a `ReplaceOperation` configured with:  
         * scope: `all`  
         * match pattern: `Theme.setLoadedStyleName`  
         * replacement: `(function(_){})`
4. Add the `modifyPrimeNgPlugin` instance to the Webpack `plugins` array.

Example webpack.config.js

```javascript
const { ModifySourcePlugin, ReplaceOperation } = require('modify-source-webpack-plugin')
...
const modifyPrimeNgPlugin = new ModifySourcePlugin({
  rules: [
    {
      test: (module) => {
        return module.resource && module.resource.includes('primeng')
      },
      operations: [
        new ReplaceOperation(
          'all',
          'document\\.createElement\\(([^)]+)\\)',
          'document.createElementFromPrimeNg({"this": this, "arguments": Array.from(arguments), element: $1})'
        ),
        new ReplaceOperation('all', 'Theme.setLoadedStyleName', '(function(_){})')
      ]
    }
  ]
})
module.exports = {
  ...webpackConfig,
  plugins: [...plugins, modifyPrimeNgPlugin]
}
```
