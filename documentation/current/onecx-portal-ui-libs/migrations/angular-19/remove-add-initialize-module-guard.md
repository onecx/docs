# Remove addInitializeModuleGuard()

In OneCX v6, `addInitializeModuleGuard()` has been removed. Translations are now handled by `TranslationConnectionService`.

## [](#%5Fupdate%5Fimports%5Fand%5Fproviders)Update imports and providers

* Remove the `addInitializeModuleGuard()` guard wrapper from router configuration.
* Register routes using `RouterModule.forRoot(routes)` and `RouterModule.forChild(routes)`.
* If the module imports `AngularAcceleratorModule` from `@onecx/angular-accelerator`, no further changes are required.
* Otherwise, add `provideTranslationConnectionService()` from `@onecx/angular-utils` to the module’s `providers` list.

| |  AngularAcceleratorModule already provides TranslationConnectionService |
| ------------------------------------------------------------------------- |

### [](#%5Fexample)Example

Before

```typescript
@NgModule({
  imports: [
    RouterModule.forRoot(addInitializeModuleGuard(routes)),
  ],
})
export class AppModule {}
```

After

```typescript
import { provideTranslationConnectionService } from '@onecx/angular-utils';

@NgModule({
  imports: [
    RouterModule.forRoot(routes),
  ],
  providers: [
    provideTranslationConnectionService(),
  ],
})
export class AppModule {}
```
