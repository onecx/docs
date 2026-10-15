# PrimeNG Theming Customization

## [](#how-primeNG-is-themed)How PrimeNG is themed in OneCX

OneCX themes define the design tokens that PrimeNG consumes. When a PrimeNG application runs as a microfrontend or remote component, register `provideThemeConfig()` so the active OneCX theme is mapped to PrimeNG in that runtime. If the runtime needs application-specific overrides, pass them through `provideThemeConfig({ overrides })`.

### [](#microfrontend)Microfrontend

Register the provider in the microfrontend’s remote module:

my-mfe-remote.module.ts

```typescript
import { provideThemeConfig } from '@onecx/angular-utils/theme/primeng'
...
@NgModule({
  providers: [
    provideThemeConfig()
  ]
})
export class MyMfe {}
```

### [](#remote-component)Remote component

Add the provider to the `bootstrapRemoteComponent` providers array in `bootstrap.ts`:

remote-component.bootstrap.ts

```typescript
import { provideThemeConfig } from '@onecx/angular-utils/theme/primeng'

bootstrapRemoteComponent(RemoteComponent, 'my-remote-component', environment.production, [
  provideThemeConfig()
])
```

### [](#microfrontend-and-remote-component-overrides)Microfrontend and remote-component overrides

If a microfrontend or remote component needs to adjust PrimeNG design tokens for its own UI, pass an `overrides` object to `provideThemeConfig({ overrides })`. Use the same structure as PrimeNG presets.

The object containing overrides must have the same structure as [PrimeNG’s presets](https://primeng.org/theming#definepreset). The presets can contain general variables like primary color or surface color, but it is also possible to define customizations for components.

Each PrimeNG component specifies a list of design tokens (e.g. [button component design tokens](https://v21.primeng.org/button#Buttonclasses)). Those can be used to override certain styles of each component.

## [](#related)Related

* [Theming](../../concepts/theming.html) — the concept page for how OneCX theming works and the theme variables available on the page.
