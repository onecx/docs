# OneCX Multi-language Translations

## [](#overview)Overview

This document contains instructions on how to set up multi-language translations in a [OneCX-compatible](../../migration/vanilla-to-onecx-angular.html) application using the `@ngx-translate` library.

## [](#prerequisites)Prerequisites

Before proceeding, complete the [Required Setup](../../setup/required/index.html) and confirm the application versions against [Platform & Package Compatibility Requirements](../../setup/required/platform-package-compatibility.html).

## [](#setup)Setup

To set up the multi-language translations support follow the steps listed below.

### [](#install-ngx-translate)Step 1: Install ngx-translate Library

The `@ngx-translate/core` package has to be installed in the project.

```bash
npm i @ngx-translate/core
```

| |  Use the caret range described in [Package Sharing Convention](../../setup/required/platform-package-compatibility.html#package-sharing-convention) for the @ngx-translate/core entry in package.json. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#share-ngx-translate)Step 2: Share ngx-translate through Remote Package Sharing

Share `@ngx-translate/core` according to [Configure Remote Package Sharing](../../setup/required/configure-remote-package-sharing.html). The package must participate in the application’s share scope so the app and the shell reuse the same `@ngx-translate/core` instance.

### [](#create-translation-files)Step 3: Create Translation Files

Create translation files (e.g. en.json, de.json) in a directory such as assets/i18n/. These files will contain key-value pairs for each language.

en.json

```json
{
  "HELLO": "Hello",
  "WELCOME": "Welcome"
}
```

### [](#import-utilities)Step 4: Import Required Utilities

In your remote module file, import the following:

remote.module.ts

```typescript
import { provideTranslateService, provideTranslateLoader, provideMissingTranslationHandler } from '@ngx-translate/core';
import { OnecxTranslateLoader, MultiLanguageMissingTranslationHandler, provideTranslationPathFromMeta } from '@onecx/angular-utils';
```

### [](#provide-translations)Step 5: Provide Translations with OnecxTranslateLoader

Translations are provided through `provideTranslateService()` from `@ngx-translate/core` combined with the `OnecxTranslateLoader` configured via `provideTranslateLoader()`. Add the provider to the module’s `providers` array:

remote.module.ts

```typescript
providers: [
  ...
  provideTranslateService({
    defaultLanguage: 'en',
    loader: provideTranslateLoader(OnecxTranslateLoader),
    missingTranslationHandler: provideMissingTranslationHandler(MultiLanguageMissingTranslationHandler)
  }),
  ...
]
```

To support multiple locales at the same time when the current locale is missing a translation, keep the `MultiLanguageMissingTranslationHandler` in the `missingTranslationHandler` slot as shown above.

| |  The provideTranslateService() \+ OnecxTranslateLoader mechanism shown here is available from OneCX UI libraries v7 (Angular 20) onward and is the approach for the current v8 end-state. On earlier versions (up to v6, Angular 19) the translation service was still provided with the createTranslateLoader factory rather than provideTranslateService(). To bring an older app to the setup on this page, follow [the OnecxTranslateLoader migration](../../../onecx-portal-ui-libs/migrations/angular-20/migrate-to-onecx-translate-loader.html) within the version-specific upgrade guides. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#provide-translation-connection)Step 6: Provide the Translation Connection Service

The translation connection service replaces the older route setup. In OneCX UI libraries v6, `addInitializeModuleGuard()` was removed; see [Remove addInitializeModuleGuard](../../../onecx-portal-ui-libs/migrations/angular-19/remove-add-initialize-module-guard.html). If the module imports `AngularAcceleratorModule` from `@onecx/angular-accelerator`, it already provides `TranslationConnectionService`. Otherwise, add `provideTranslationConnectionService()` from `@onecx/angular-utils` to the module’s `providers` list:

remote.module.ts

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
```

| |  provideTranslationConnectionService() is available from OneCX UI libraries v6 (Angular 19) onward and replaces the addInitializeModuleGuard() route wrapper removed in v6\. Apps on earlier versions still use that wrapper and reach this setup by following the version-specific upgrade guides. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#provide-translation-path)Step 7: Provide Translation Path

Use provideTranslationPathFromMeta(import.meta.url, …​) to specify the location of your translation files:

remote.module.ts

```typescript
providers: [
  ...
  provideTranslationPathFromMeta(import.meta.url, 'assets/i18n/'),
  ...
]
```

| |  Replace 'assets/i18n/' with the actual path to your translation files if different. |
| -------------------------------------------------------------------------------------- |

| |  If the error "Cannot construct translation path from local file path. Please check whether the webpack configuration for importMeta is correct: [https://webpack.js.org/configuration/module/#moduleparserjavascriptimportmeta"](https://webpack.js.org/configuration/module/#moduleparserjavascriptimportmeta)appears, it means either the provider is used in the application and import.meta.url incorrectly resolves to a local file:// path. or the application does not use provideTranslationPathFromMeta, but is likely using a newer Angular version than the shell or preloader. In this case, modules are loaded from the app’s context, which also leads to a local file:// prefix. To fix this, this line has to be added to module.exports in the webpack.config.js: webpack.config.ts module.exports = {  ...   module: { parser: { javascript: { importMeta: false } } }, } |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#feature-modules)Step 8: Support in Feature Modules

If any feature modules use ngx-translate features (e.g. translate pipe), ensure TranslateModule is also imported in those modules:

feature.module.ts

```typescript
@NgModule({
  imports: [
    ...
    TranslateModule,
    ...
  ]
})
export class FeatureModule {}
```

## [](#completion-checklist)Completion Checklist

To verify that the setup is complete, ensure the following:

* `@ngx-translate/core` is installed and listed in `package.json` with a `^` sign.
* Webpack configuration includes `@ngx-translate/core` as a shared package.
* Translation files are created and accessible.
* `provideTranslateService()` with `provideTranslateLoader(OnecxTranslateLoader)` is configured in the remote module.  
   * (Optional) `MultiLanguageMissingTranslationHandler` is set up for full multi-language support.
* `provideTranslationConnectionService()` is provided when the module does not import `AngularAcceleratorModule`.
* `provideTranslationPathFromMeta` is used to specify the translation files' path.
* `TranslateModule` is imported in any feature modules using translation features.

## [](#next-steps)Next Steps

After completing the setup, you can start using translations in your components and templates. For usage instructions, refer to the [multi-language usage document](multi-language-usage.html).
