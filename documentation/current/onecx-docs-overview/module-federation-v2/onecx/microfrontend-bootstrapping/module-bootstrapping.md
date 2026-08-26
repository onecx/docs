# Module Bootstrapping and Configuration

The following requirements need to be fulfilled when exposing modules using the Webcomponent method:

1. Webpack configuration needs to expose the **main.ts** file of the module.
2. The **main.ts** file of the module needs to bootstrap the module asynchronously.
3. Module bootstrapping has to cover [Angular issues](../../concepts/webcomponents/expose-content-as-webcomponent.html#angular%5Fissues) (for Angular-based modules only)
4. Module class  
   1. needs to register an entry point as a Custom Element in the Custom Elements Registry.  
   2. needs to adapt routing so Shell registers routing happening within the module.  
   3. needs to adapt configuration, so services are using correct URLs to external resources.

Below, a module setup example (Angular-based) for using the Webcomponent expose method is presented. Each file’s content is going to be explained in detail, with important context information for technologies other than those presented.

webpack.config.js

```typescript
const config = withModuleFederationPlugin({
  name: 'example-ui',
  filename: 'remoteEntry.js',
  exposes: {
    './ExampleModule': './src/main.ts'
  },
  ...
})
```

Webpack configuration is exposing a **main.ts** file.

src/main.ts

```typescript
import('./bootstrap').catch((err) => console.error(err))
```

The **main.ts** file is importing (asynchronously) the **bootstrap.ts** file.

src/bootstrap.ts

```typescript
import { bootstrapModule } from '@onecx/angular-webcomponents'
import { environment } from './environments/environment'
import { ExampleModule } from './app/module'

bootstrapModule(ExampleModule, 'microfrontend', environment.production)
```

The **bootstrap.ts** file is bootstrapping the module using @onecx/angular-webcomponents library to ensure that [Angular ngZone and platform are shared](../../concepts/webcomponents/expose-content-as-webcomponent.html#angular%5Fissues) (Angular requirement only). For other technologies, simply call any asynchronous bootstrap function required.

src/app/module.ts

```typescript
import { HttpClient, provideHttpClient, withInterceptorsFromDi } from '@angular/common/http'
import { APP_INITIALIZER, DoBootstrap, Injector, NgModule } from '@angular/core'
import { Router, RouterModule, Routes } from '@angular/router'
import { BrowserModule } from '@angular/platform-browser'
import { BrowserAnimationsModule } from '@angular/platform-browser/animations'
import { CommonModule } from '@angular/common'
import { MissingTranslationHandler, TranslateLoader, TranslateModule } from '@ngx-translate/core'
import {
  AppStateService,
  ConfigurationService,
  createTranslateLoader,
  PortalCoreModule,
  PortalMissingTranslationHandler,
  PortalApiConfiguration,
} from '@onecx/portal-integration-angular'
import { AngularAuthModule } from '@onecx/angular-auth'
import { createAppEntrypoint, initializeRouter, startsWith } from '@onecx/angular-webcomponents'
import { addInitializeModuleGuard } from '@onecx/angular-integration-interface'
import { Configuration } from './shared/generated'

@Component({
  selector: 'app-root',
  template: `<router-outlet></router-outlet>`
})
export class AppEntrypointComponent {}

export const routes: Routes = [
  {
    matcher: startsWith(''),
    loadChildren: () => import('./feature/feature.module').then((mod) => mod.FeatureModule)
  },
  {
    matcher: startsWith('tracking'),
    loadChildren: () => import('./tracking/tracking.module').then((mod) => mod.TrackingModule)
  }
]

function apiConfigProvider(configService: ConfigurationService, appStateService: AppStateService) {
  return new PortalApiConfiguration(Configuration, environment.apiPrefix, configService, appStateService)
}

@NgModule({
    declarations: [AppEntrypointComponent],
    imports: [
        CommonModule,
        PortalCoreModule.forMicroFrontend(),
        RouterModule.forRoot(addInitializeModuleGuard(routes)),
        TranslateModule.forRoot({
        extend: true,
        isolate: false,
        loader: {
            provide: TranslateLoader,
            useFactory: createTranslateLoader,
            deps: [HttpClient, AppStateService]
        },
        missingTranslationHandler: {
            provide: MissingTranslationHandler,
            useClass: PortalMissingTranslationHandler
        }
        }),
        BrowserModule,
        AngularAuthModule,
        BrowserAnimationsModule,
    ],
    exports: [],
    providers: [
        {
            provide: Configuration,
            useFactory: apiConfigProvider,
            deps: [ConfigurationService, AppStateService]
        },
        {
            provide: APP_INITIALIZER,
            useFactory: initializeRouter,
            multi: true,
            deps: [Router, AppStateService]
        },
        provideHttpClient(withInterceptorsFromDi())
    ]
})
export class ExampleModule implements DoBootstrap {
    constructor(private readonly injector: Injector) {}

    ngDoBootstrap(): void {
        createAppEntrypoint(AppEntrypointComponent, 'example-webcomponent', this.injector)
    }
}
```

__Table 1\. Navigation__
| [← Previous: Microfrontend Bootstrapping](index.html) | [Next: Module Example Deep Dive →](module-deep-dive.html) |
| ----------------------------------------------------- | --------------------------------------------------------- |
