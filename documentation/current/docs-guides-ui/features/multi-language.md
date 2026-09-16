# Multi-language

An Angular application’s translations may not cover every language a user could end up in — a key can be missing for the user’s current language, or a library shared into the application may not ship a translation for it at all. Instead of showing the raw translation key in this situation, an Angular OneCX application can opt into fallback languages: additional languages that are tried, in order, before giving up and displaying the key.

This feature builds on the [Translations](../concepts/translations.html) concept — it does not replace the regular translation lookup, it only decides what happens when that lookup fails.

## [](#how-it-works)How it works

Angular OneCX applications are set up with `` @onecx/angular-utils’s `MultiLanguageMissingTranslationHandler `` as the `ngx-translate` `MissingTranslationHandler` (see [Multi-language Translations — Setup](../angular/translation/multi-language-setup.html), Step 6). When a translation key cannot be resolved in the current language, the handler builds a list of candidate fallback languages and tries them one after another until one produces a value:

* If the user’s profile has explicit language settings (`settings.locales`, exposed via the [UserService](../../onecx-portal-ui-libs/libraries/angular-integration-interface.html#user-service)), those languages are used, in the order given.
* Otherwise, the browser’s configured languages (`navigator.languages`) are used, normalized to the application’s supported locale format.

For each candidate language, the handler first reloads the application’s own translations for that language and looks up the key. If the key is still not found, it falls back to translations exposed by libraries shared into the application (resolved via `DynamicTranslationService`, using the library/app identifiers registered through `provideMultiLanguageIdentifier` — see below) and looks up the key there. As soon as a language produces a value, that value is used, interpolated with any translation parameters. If none of the candidate languages resolve the key, the original behavior applies and the translation key itself is displayed, along with a logged error.

## [](#configuration)Configuration

Fallback languages are enabled by providing `MultiLanguageMissingTranslationHandler` as the `missingTranslationHandler` when configuring `TranslateModule.forRoot()`, as shown in the [setup document](../angular/translation/multi-language-setup.html):

```typescript
import { MultiLanguageMissingTranslationHandler } from '@onecx/angular-utils'

imports: [
  ...
  TranslateModule.forRoot({
    isolate: false,
    loader: {
      provide: TranslateLoader,
      useFactory: createTranslateLoader,
      deps: [HttpClient]
    },
    missingTranslationHandler: {
      provide: MissingTranslationHandler,
      useClass: MultiLanguageMissingTranslationHandler
    }
  }),
  ...
]
```

### [](#registering-library-translations-for-fallback-lookup)Registering library translations for fallback lookup

To let the handler fall back to a library’s own translations (rather than only the application’s), register the library (or application) as a multi-language identifier with `provideMultiLanguageIdentifier`:

```typescript
import { provideMultiLanguageIdentifier } from '@onecx/angular-utils'

providers: [
  ...
  provideMultiLanguageIdentifier('my-shared-lib', '1.0.0', 'lib'),
  ...
]
```

An application identifier is registered automatically from the application’s element name when none is provided explicitly, so this step is only required for libraries that expose their own translations and should participate in the fallback lookup.

## [](#related)Related

* [Translations](../concepts/translations.html) — the underlying translation-lookup mechanism this feature falls back on.
* [Multi-language Translations — Setup](../angular/translation/multi-language-setup.html) — full Angular setup, including where the missing-translation handler is wired in.
