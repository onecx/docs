# Add Webpack Plugin for Angular Material

In OneCX v6, applications using Angular Material or Angular CDK must add a Webpack plugin. This change is required after upgrading to Angular 19.

| |  This setup will be replaced by a OneCX-provided Webpack plugin in a future version. |
| -------------------------------------------------------------------------------------- |

## [](#%5Finstall%5Fand%5Fconfigure%5Fwebpack%5Fplugin)Install and Configure Webpack Plugin

1. Install `modify-source-webpack-plugin`  
```bash  
npm install modify-source-webpack-plugin --save-dev  
```
2. Import `ModifySourcePlugin` and `ReplaceOperation` from `` modify-source-webpack-plugin`in `webpack.config.js ``
3. Create a `modifyMaterialPlugin` instance with a rules array containing one rule object:  
   * The rule must define a `test` function that returns `true` when `module.resource` exists and the resource path includes `@angular/material` or `@angular/cdk`.  
   * The rule must include an `operations` array with a `ReplaceOperation` configured with:  
         * scope: `all`  
         * match pattern: `document\.createElement\(`  
         * replacement: `document.createElementFromMaterial({"this": this, "arguments": Array.from(arguments)},`
4. Add the `modifyMaterialPlugin` instance to the Webpack `plugins` array.

Example webpack.config.js

```javascript
const { ModifySourcePlugin, ReplaceOperation } = require('modify-source-webpack-plugin')

const modifyMaterialPlugin = new ModifySourcePlugin({
  rules: [
    {
      test: (module) => {
        return (
          module.resource &&
          (module.resource.includes('@angular/material') ||
            module.resource.includes('@angular/cdk'))
        )
      },
      operations: [
        new ReplaceOperation(
          'all',
          'document\\.createElement\\(',
          'document.createElementFromMaterial({"this": this, "arguments": Array.from(arguments)},'
        )
      ]
    }
  ]
})

module.exports = {
  ...webpackConfig,
  plugins: [...plugins, modifyMaterialPlugin]
}
```
