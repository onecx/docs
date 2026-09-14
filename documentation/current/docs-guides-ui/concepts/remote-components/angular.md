# Remote Components in Angular Applications

This page covers the Angular-specific APIs for exposing and hosting Remote Components. See [Remote Components](../remote-components.html) for the shared concept and terminology.

## [](#exposing-an-angular-remote-component)Exposing a Remote Component

An Angular Remote Component is bootstrapped as a standalone Custom Element via `bootstrapRemoteComponent()` from `@onecx/angular-webcomponents`, which handles the platform concerns a Remote Component needs that a regular Angular application does not — sharing `NgZone` and the platform with the host page, and connecting to the Remote Component’s own router context.

```typescript
bootstrapRemoteComponent(
  ExampleComponent,
  'example-remote-component',
  environment.production,
  providers
)
```

To receive its configuration once the host places it in a Slot, the component implements the `ocxRemoteComponent` interface from `@onecx/angular-remote-components`:

```typescript
import { ocxRemoteComponent, RemoteComponentConfig } from '@onecx/angular-remote-components';

export class ExampleComponent implements ocxRemoteComponent {
  ocxInitRemoteComponent(config: RemoteComponentConfig): void {
    // config.appId, config.productName, config.baseUrl, config.permissions
  }
}
```

The full walkthrough — bootstrap files, webpack configuration, and the complete component example — is covered in [Component Approach](../../setup/required/expose-remote-module/component-approach.html).

## [](#hosting-a-slot-in-angular)Hosting a Slot

To render a Slot inside an Angular application, import `AngularRemoteComponentsModule` (from `@onecx/angular-remote-components`) and use the `<ocx-slot>` component:

```html
<ocx-slot
  name="onecx-shell-header-actions"
  [inputs]="{ title: 'Remote title' }"
  [outputs]="{ onSelect: onSelectHandler }"
></ocx-slot>
```

`<ocx-slot>` accepts:

| Input   | Type                                  | Description                                                              |
| ------- | ------------------------------------- | ------------------------------------------------------------------------ |
| name    | string                                | Required. The name of the Slot to resolve Remote Components for.         |
| inputs  | Record<string, unknown>               | Data passed down to every Remote Component rendered inside the slot.     |
| outputs | Record<string, RemoteComponentOutput> | Event handlers bound to every Remote Component rendered inside the slot. |

Behind the scenes, `<ocx-slot>` uses `SlotService` to resolve which Remote Component(s), if any, are assigned to the named slot for the current workspace, loads each one via module federation, and mounts it — applying the same [style isolation](../style-isolation.html) used for any other application content.

## [](#related)Related

* [Remote Components](../remote-components.html) — the shared concept, terminology, and workspace-administration behavior.
* [Component Approach](../../setup/required/expose-remote-module/component-approach.html) — the complete, practical how-to for exposing an Angular Remote Component.
