# Adjust ngrx utilities usage

In OneCX v8, some `@onecx/ngrx-accelerator` utility names changed. If your app still uses the old utility names, TypeScript compilation fails after upgrade.

| |  This adaptation is required only if you changed generated code, added custom ngrx implementation, or if your project is affected by these renamed utilities as a breaking change. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

## [](#%5Frequired%5Frename)Required rename

* `filterForQueryParamsChanged` → `filterOutQueryParamsHaveNotChanged`
* `filterForOnlyQueryParamsChanged` → `filterOutOnlyQueryParamsChanged`

## [](#%5Fexample)Example

Before

```typescript
import {
  filterForQueryParamsChanged,
  filterForOnlyQueryParamsChanged,
} from '@onecx/ngrx-accelerator'
```

After

```typescript
import {
  filterOutQueryParamsHaveNotChanged,
  filterOutOnlyQueryParamsChanged,
} from '@onecx/ngrx-accelerator'
```
