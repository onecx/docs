# Update package imports for PrimeNG theming

In version 7, the PrimeNG theming utilities have been moved to a separate subpackage:`@onecx/angular-utils/theme/primeng` within the `@onecx/angular-utils` library.

## [](#%5Fupdate%5Fimport%5Fpath)Update import path

Please update all imports related to PrimeNG theming utilities to use the new package.

Before

```typescript
import { provideThemeConfig } from '@onecx/angular-utils'
```

After

```typescript
import { provideThemeConfig } from '@onecx/angular-utils/theme/primeng'
```

## [](#%5Fprimeng%5Fsubpackage%5Fpublic%5Fapi%5Fcontents)PrimeNG subpackage public API contents

### [](#%5Fclasses)Classes

* `CustomUseStyle`
* `ThemeConfigService`

### [](#%5Ffunctions)Functions

* `adjustColor`
* `colorDelta`
* `createPalette`
* `normalizeKeys`
* `provideThemeConfig`
* `provideThemeConfigService`

### [](#%5Fconstants)Constants

* `CustomPreset`
* `standardColorAdjustment`

### [](#%5Finjection%5Ftokens)Injection Tokens

* `IS_ADVANCED_THEMING`
* `THEME_OVERRIDES`

### [](#%5Finterfaces)Interfaces

* `ColorAdjustment`
* `ThemeConfigProviderOptions`

### [](#%5Ftypes)Types

* `ThemeOverrides`
