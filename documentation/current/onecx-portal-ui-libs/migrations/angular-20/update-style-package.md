# Update package imports for style utilities

In version 7, the style utilities have been moved to a separate subpackage:`@onecx/angular-utils/style` within the `@onecx/angular-utils` library.

## [](#%5Fupdate%5Fimport%5Fpath)Update import path

Please update all imports related to micro-frontend and remote component style utilities to use the new package.

Before

```typescript
import { updateStylesForMfeChange } from '@onecx/angular-utils'
```

After

```typescript
import { updateStylesForMfeChange } from '@onecx/angular-utils/style'
```

## [](#%5Fstyle%5Fsubpackage%5Fpublic%5Fapi%5Fcontents)Style subpackage public API contents

### [](#%5Ffunctions)Functions

* `addStyleToHead`
* `createApplicationScopedCss`
* `createCssRequestHeaders`
* `createStyleUsedByMfeRc`
* `fetchAppCss`
* `getAllStylesUsedByKey`
* `getAppStyleByScope`
* `getStyleUsageCount`
* `getStyleUsageCountForRc`
* `isResponseValidCss`
* `isStyleUsedByMfe`
* `removeAllMfeUsagesFromStyles`
* `removeAllRcUsagesFromStyles`
* `removeMfeUsageFromStyle`
* `removeRcUsageFromStyle`
* `replaceRootAndHtmlWithScope`
* `replaceRootWithScope`
* `replaceStyleContent`
* `slotNameToPropertyName`
* `updateStylesForMfeChange`
* `updateStylesForRcCreation`
* `useStyleForMfe`
* `useStyleForRc`

### [](#%5Fconstants)Constants

* `dataAppStylesAttribute`
* `dataAppStylesKey`
* `dataMfeStylesAttribute`
* `dataMfeStylesKey`
* `dataRcStylesAttribute`
* `dataRcStylesKey`
* `dataRcStylesStart`
* `dataShellStylesAttribute`
* `dataShellStylesKey`
