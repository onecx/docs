# Migrate to <code>OnecxTranslateLoader</code>

In v7, the translation loading mechanism in `@onecx/angular-utils` has been refactored.

The following items have been **removed**:

* `AsyncTranslateLoader` class
* `createTranslateLoader` function

The following item has been **added** and must now be used for translation:

* `OnecxTranslateLoader` class

All applications need to migrate to this new loader and the new way of providing `TranslateService`. Please follow the steps below to update your application.

## [](#%5Frequired%5Fmigration%5Fsteps)Required migration steps

* Remove all imports and usages of:  
   * `AsyncTranslateLoader`  
   * `createTranslateLoader`
* Update `module.ts` to provide translation using the new mechanism
* Replace existing loader configuration with `OnecxTranslateLoader`

## [](#%5Fprovide%5Ftranslation%5Fusing%5Fonecxtranslateloader)Provide translation using `OnecxTranslateLoader`

With the removal of `createTranslateLoader` and `AsyncTranslateLoader`, translation loading is handled through `provideTranslateService()` from `@ngx-translate/core`, combined with the `OnecxTranslateLoader`. Please change the way your application is providing translation loader in `module.ts` file.

### [](#%5Fbefore)Before

Previously, translation was provided using factory-based loader:

```ts
@NgModule({
  declarations: [AppEntrypointComponent],
  imports: [
    ...
    TranslateModule.forRoot({
      isolate: true,
      loader: { provide: TranslateLoader, useFactory: createTranslateLoader, deps: [HttpClient] },
      missingTranslationHandler: {
        provide: MissingTranslationHandler,
        useClass: AngularAcceleratorMissingTranslationHandler
      }
    })
    ...
  ],
  providers: [
    ...
  ]
})
```

### [](#%5Fafter)After

Now you must use `provideTranslateService()` and configure `OnecxTranslateLoader` via `provideTranslateLoader()`:

```ts
@NgModule({
  declarations: [AppEntrypointComponent],
  imports: [
    ...
  ],
  providers: [
    ...
    provideTranslateService({
      defaultLanguage: 'en',
      loader: provideTranslateLoader(OnecxTranslateLoader),
      missingTranslationHandler: provideMissingTranslationHandler(MultiLanguageMissingTranslationHandler)
    }),
    ...
  ]
})
```

## [](#%5Fupdate%5Fapp%5Fcomponent%5Fts%5Finjection%5Fto%5Fdi%5Fpattern%5Frecommended)Update `app.component.ts` injection to DI pattern (Recommended)

`TranslateService` should no longer be injected via constructor. The recommended way is using Angular’s `inject()` function.

Injection Example 

Before

```ts
import { Component} from '@angular/core'
import { TranslateService } from '@ngx-translate/core'
import { PrimeNG } from 'primeng/config'
import { UserService } from '@onecx/angular-integration-interface'

@Component({
  standalone: false,
  selector: 'ocx-shell-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  title = 'shell'

  constructor(
    private readonly translateService: TranslateService,
    private readonly config: PrimeNG,
    private readonly userService: UserService
  ) {}

  ...
}
```

After

```ts
import { Component, inject } from '@angular/core'
import { TranslateService } from '@ngx-translate/core'
import { PrimeNG } from 'primeng/config'
import { UserService } from '@onecx/angular-integration-interface'

@Component({
  standalone: false,
  selector: 'ocx-shell-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  title = 'shell'

  private readonly translateService: TranslateService = inject(TranslateService)
  private readonly config: PrimeNG = inject(PrimeNG)
  private readonly userService: UserService = inject(UserService)

  ...
}
```
