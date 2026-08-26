# Provide ThemeConfig

| |  These changes are required for apps using PrimeNG only. |
| ---------------------------------------------------------- |

Since version 6 of OneCX to apply PrimeNG theming it is required to add an additional provider to the Microfrontends and Remote Components.

## [](#%5Fmicrofrontend%5Ftheme%5Fconfiguration)Microfrontend theme configuration

* import `provideThemeConfig` provider from `@onecx/angular-utils` in `module.ts` file
* define `provideThemeConfig` provider in `NgModule` `providers` array

micro-frontend-remote.module.ts

```typescript
import { provideThemeConfig } from '@onecx/angular-utils'
...
@NgModule({
    providers: [
        provideThemeConfig()
    ]
}) export class MyMfe {}
```

## [](#%5Fremote%5Fcomponents%5Ftheme%5Fconfiguration)Remote components theme configuration

* import `provideThemeConfig` provider from `@onecx/angular-utils` in `bootstrap.ts` file
* define `provideThemeConfig` in `bootstrapRemoteComponent` function `providers` array from `@onecx/angular-webcomponents`

remote-component.bootstrap.ts

```typescript
import { provideThemeConfig } from '@onecx/angular-utils'

bootstrapRemoteComponent(RemoteComponent, 'my-remote-component', environment.production, [
  provideThemeConfig()
])
```

## [](#theme-overrides)Provide theme overrides

In angular 19+ OneCX is creating its own theme presets per App that utilize PrimeNG theming. If the look and feel of some PrimeNG components is not matching the expectations, developers should use theme overrides to change them.

More about how to override the theme elements can be found in [theming documentation](https://onecx.github.io/docs/documentation/current/docs-guides-ui/angular/theming.html).
