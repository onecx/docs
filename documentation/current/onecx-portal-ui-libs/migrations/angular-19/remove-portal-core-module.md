# Remove PortalCoreModule

In OneCX v6, `PortalCoreModule` has been replaced with `AngularAcceleratorModule`.

## [](#%5Fupdate%5Fimports)Update imports

* Replace all imports of `PortalCoreModule` from '@onecx/portal-integration-angular' with `AngularAcceleratorModule` from `@onecx/angular-accelerator`.
* Replace `PortalCoreModule` (also `PortalCoreModule.forRoot()`, `PortalCoreModule.forMicroFrontend()`) with `AngularAcceleratorModule`.

### [](#%5Fexample)Example

Before

```typescript
import { PortalCoreModule } from "@onecx/portal-integration-angular";

@Component({
  standalone: true,
  imports: [PortalCoreModule]
})
```

After

```typescript
import { AngularAcceleratorModule } from "@onecx/angular-accelerator";

@Component({
  standalone: true,
  imports: [AngularAcceleratorModule]
})
```

## [](#remove-portal-integration-angular)Remove '@onecx/portal-integration-angular'

`@onecx/portal-integration-angular` is no longer available in OneCX v6 and must be completely removed from the application at this point.

### [](#%5Fverify%5Fall%5Fimports%5Fare%5Fmigrated)Verify All Imports Are Migrated

Before removing the package, ensure that all imports from `@onecx/portal-integration-angular` have been removed or properly migrated to their new locations as outlined in the [Update Component Imports](update-component-imports.html#update-component-imports) section.

### [](#%5Funinstall%5Fthe%5Fpackage)Uninstall the Package

Once all imports have been migrated, remove the deprecated package:

```bash
npm uninstall @onecx/portal-integration-angular
```
